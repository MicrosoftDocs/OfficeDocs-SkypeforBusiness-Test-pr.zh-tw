---
title: Lync Server 2013：行動技術需求
TOCTitle: 行動技術需求
ms:assetid: 831be681-4de0-4e42-b04f-8879ca4dcd23
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690030(v=OCS.15)
ms:contentKeyID: 49291507
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 行動技術需求

 

_**上次修改主題的時間：** 2014-07-24_

    Some information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.

行動使用者會遇到各種需要特別規劃的行動應用程式案例。例如，某人下班時，可能會透過 3G 網路連線，開始使用行動應用程式，上班時再切換至公司的 Wi-Fi 網路，離開辦公室時再切換回 3G。您需要規劃環境來支援像這樣的網路轉換，以確保一致的使用者經驗。本節說明支援行動應用程式和自動探索行動資源時，必須具備的基礎結構需求。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然行動應用程式也可以連線至其他 Lync Server 2013 服務，但是這個將所有行動應用程式 Web 要求傳送至相同外部 Web 完整網域名稱 (FQDN) 的需求，僅適用於 Lync Server 2013 Mobility Service。其他行動服務不需要此設定。</td>
</tr>
</tbody>
</table>


如果您使用 Lync Server 2013 提供的 Lync Mobile，硬體負載平衡器的 Cookie 相關性要求將大幅減少，而且您可以替換傳輸控制通訊協定 (TCP) 相關性。雖然仍然可以使用 Cookie 相關性，但是 Web 服務不再需要此相關性。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>無論起始點是在內部或外部，所有 Mobility Service 流量都是通過反向 Proxy 傳輸。對於單一反向 Proxy 或一個反向 Proxy 陣列，或對於提供反向 Proxy 功能的裝置，當內部流量傳出介面並嘗試立即在相同介面接收時，會發生問題。這通常會導致違反安全性規則，稱為 TCP 封包詐騙或僅稱詐騙。必須允許「U 型迴轉」 (傳出和立即接收封包或一系列封包)，以供行動性正常運作。有一個解決此問題的方法是使用與防火牆相隔離的反向 Proxy (基於安全因素，應該在防火牆上一律強制執行此詐騙預防規則)。U 型迴轉會發生在反向 Proxy 的外部介面上，而非防火牆外部介面。您可以在防火牆上偵測到詐騙，並在反向 Proxy 放寬規則，以允許該行動性所需要的傳回。<br />
儘可能使用網域名稱系統 (DNS) 主機或 CNAME 記錄來定義反向 Proxy 如何處理傳回行為 (而非防火牆)。</td>
</tr>
</tbody>
</table>


Lync Server 2013 支援 Lync 2010 Mobile 和 Lync 2013 行動用戶端的行動服務。兩個用戶端會使用 Lync Server 2013 自動探索服務找出其行動進入點，但根據其使用的行動服務而有所不同。 Lync 2010 Mobile 會使用 Lync Server 2010 累計更新 (2011 年 11 月) 所導入的 Mobility Service，稱為 *Mcx* 。 Lync 2013 行動用戶端使用 Unified Communications Web API 或 *UCWA* ，做為其行動服務提供者。

## 內部及外部 DNS 組態

Mobility Services Mcx (在 Lync Server 2010 累計更新 (2011 年 11 月) 導入) 以及 UCWA (在 Lync Server 2013 累計更新 (2013 年 2 月) 導入) 以相同方式使用 DNS。

當您使用自動探索時，行動裝置會使用 DNS 尋找資源。在 DNS 查閱期間，會先嘗試連線至與內部 DNS 記錄 (lyncdiscoverinternal.*\<internal domain name\>*) 相關聯的 FQDN。如果無法使用內部 DNS 記錄來建立連線，則會嘗試使用外部 DNS 記錄 (lyncdiscover.*\<sipdomain\>*) 來進行連線。在網路內部的行動裝置會連線至內部自動探索服務 URL，而在網路外部的行動裝置會連線至外部自動探索服務 URL。外部自動探索要求會通過反向 Proxy。Lync Server 2013 自動探索服務會針對使用者的主集區，傳回所有 Web 服務 URL，包括 Mobility Service (Mcx 和 UCWA) URL。不過，內部 Mobility Service URL 及外部 Mobility Service URL 都會與外部 Web 服務 FQDN 相關聯。因此，無論行動裝置是在網路內部或外部，該裝置都會透過反向 Proxy 從外部連線至 Lync Server 2013 Mobility Service。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>必須注意的是，您的部署可能包含內部和外部使用的多個不同命名空間。SIP 網域名稱可能與內部部署網域名稱不同。例如，SIP 網域可能是 <strong>contoso.com</strong>，而內部部署可能是 <strong>contoso.net</strong>。登入 Lync Server 的使用者將使用 SIP 網域名稱，例如 <strong>john@contoso.com</strong>。處理外部 Web 服務 (在 拓撲產生器 中定義為 [外部 Web 服務]) 時，網域名稱和 SIP 網域名稱將與 DNS 中定義的名稱一致。處理內部 Web 服務 (在 拓撲產生器 中定義為 [內部 Web 服務]) 時，內部 Web 服務的預設名稱將是 前端伺服器、前端集區、Director 或 Director 集區 的 FQDN。您可以選擇覆寫內部 Web 服務名稱。對於內部 Web 服務，您應該使用內部網域名稱 (而非 SIP 網域名稱)，並定義 DNS 主機 A (對於 IPv6 則是 AAAA) 記錄來反映覆寫的名稱。例如，預設的內部 Web 服務 FQDN 可能是 <strong>pool01.contoso.net</strong>。受覆寫的內部 Web 服務 FQDN 可能是 <strong>webpool.contoso.net</strong>。以此方式定義 Web 服務有助於確保遵循服務的內部及外部位置 (而非使用服務之使用者的位置)。<br />
不過，由於 Web 服務是在 拓撲產生器 中定義，而且可以覆寫內部 Web 服務名稱，因此，只要產生的 Web 服務名稱、驗證該服務的憑證和定義該服務的 DNS 記錄三者保持一致，您就能夠以任何的網域名稱 (包括 SIP 網域名稱) 定義您所需的內部 Web 服務。最後，IP 位址的名稱解析將由 DNS 主機記錄和一致的命名空間所決定。<br />
對於本主題和範例而言，內部網域名稱是用來說明拓撲和 DNS 定義。</td>
</tr>
</tbody>
</table>


下圖說明使用內部和外部 DNS 設定時，Mobility Service 和自動探索服務的行動應用程式 Web 要求流程。

**使用自動探索的行動服務流程**

![行動要求流程](images/Hh690030.cdb96424-96f2-4abf-88d7-1d32d1010ffd(OCS.15).jpg "行動要求流程")

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此圖說明一般 Web 服務。名稱為 Mobility 的虛擬目錄說明 Mobility Services Mcx 及/或 UCWA。如果尚未套用 Lync Server 2013 累計更新 (2013 年 2 月)，您不一定會有內部與外部 Web 服務上定義的虛擬目錄 Ucwa。您會有虛擬目錄自動探索，而且可能有虛擬目錄 Mcx。<br />
無論您部署的行動服務技術為何，自動探索與服務探索會以相同方式運作。</td>
</tr>
</tbody>
</table>


如果不管是來自公司網路內部或外部行動使用者都要支援，則內部和外部 Web FQDN 都必須符合某些先決條件。此外，依據您選擇實作的功能，您可能還需要符合其他需求。

  - 新的 DNS、CNAME 或 A (主機，對於 IPv6 則為 AAAA) 記錄，適用於自動探索。

  - 新防火牆規則 (如果您想要透過 Wi-Fi 網路來支援推入通知)。

  - 內部伺服器憑證和反向 Proxy 憑證上的主體替代名稱，適用於自動探索。

  - 前端伺服器硬體負載平衡器設定變更來源相關性。

您的拓撲必須符合下列需求，才能支援 Mobility Service 和自動探索服務：

  - 前端集區內部 Web FQDN 必須與 前端集區 外部 Web FQDN 區別。

  - 內部 Web FQDN 必須只解析為公司網路內部，並且可以從公司網路內部存取。

  - 外部 Web FQDN 必須只解析為網際網路，並且可以從網際網路存取。

  - 針對在公司網路內部的使用者，Mobility Service URL 必須定址至外部 Web FQDN。此需求適用於 Mobility Service，並且只套用至這個 URL。

  - 針對在公司網路外部的使用者，要求必須傳送至 前端集區或 Director 的外部 Web FQDN。

如果您支援自動探索，則需要為每個 SIP 網域建立下列 DNS 記錄：

  - 內部 DNS 記錄，以支援從您組織網路內部連線的行動使用者。

  - 外部 (或公用) DNS 記錄，以支援從網際網路連線的行動使用者。

內部自動探索 URL 應該不能從您的網路外部定址。外部自動探索 URL 應該不能從您的網路內部定址。不過，如果您無法達到這個外部 URL 的需求，行動用戶端的功能應該不會受影響，因為一定都會先嘗試內部 URL。

DNS 記錄可以是 CNAME 記錄或 A (主機，對於 IPv6 則為 AAAA) 記錄。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>行動裝置用戶端不支援來自不同網域的多個 Secure Sockets Layer (SSL) 憑證。因此，不支援透過 HTTPS 將 CNAME 重新導向至不同的網域。例如，不支援透過 HTTPS 將 lyncdiscover.contoso.com 的 DNS CNAME 記錄重新導向至 director.contoso.net 的位址。在這樣的拓撲中，行動裝置用戶端需要使用 HTTP 來進行第一個要求，以透過 HTTP 來解析 CNAME 重新導向。後續的要求則會使用 HTTPS。若要支援此案例，您需要以連接埠 80 的 Web 發行規則來設定反向 Proxy (HTTP)。如需詳細資訊，請參閱＜ <a href="lync-server-2013-configuring-the-reverse-proxy-for-mobility.md">在 Lync Server 2013 中設定行動的反向 Proxy</a>＞中的＜建立連接埠 80 的網頁發行規則＞。<br />
支援透過 HTTPS 將 CNAME 重新導向至相同網域。在此情況下，目的地網域的憑證包含來源網域。</td>
</tr>
</tbody>
</table>


如需案例所需之 DNS 記錄的詳細資訊，請參閱＜ [Lync Server 2013 中的 DNS 摘要 - 自動探索](lync-server-2013-dns-summary-autodiscover.md)＞。

## 連接埠和防火牆需求

如果您支援推入通知，並且想要讓 Apple 行動裝置透過 Wi-Fi 網路來接收推入通知，您也需要在企業 Wi-Fi 網路上開啟連接埠 5223。連接埠 5223 是 Apple Push Notification Service (APNS) 使用的輸出 TCP 連接埠。行動裝置會啟動連線。如需詳細資訊，請參閱 [http://support.apple.com/kb/TS1629](http://support.apple.com/kb/ts1629?viewlocale=zh_tw)。

<table>
<thead>
<tr class="header">
<th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 Lync 2013 行動用戶端的 Apple 裝置不需要推入通知。</td>
</tr>
</tbody>
</table>


請注意，如果使用者隸屬於 Survivable Branch Appliance (SBA)，則需要下列連接埠：

  - UcwaSipExternalListeningPort 需要連接埠 5088

  - UcwaSipPrimaryListeningPort 需要連接埠 5089

如需自動探索之連接埠與通訊協定需求的其他詳細資訊與指示，請參閱＜ [Lync Server 2013 中的連接埠摘要 - 自動探索](lync-server-2013-port-summary-autodiscover.md)＞。

## 憑證需求

如果您支援 Lync 行動用戶端的自動探索，則需要修改憑證上的主體替代名稱清單，以支援從行動用戶端進行安全連線。您必須針對每個執行自動探索服務的 前端伺服器和 Director，要求及指派新的憑證，新增本節說明的主體替代名稱項目。建議的方法是也為反向 Proxy 修改憑證上的主體替代名稱清單。您需要針對組織中的每個 SIP 網域，新增主體替代名稱項目。

使用內部憑證授權單位重新發行憑證通常是很簡單的程序，但是將多個主體替代名稱項目新增至反向 Proxy 所使用的公開憑證可能很昂貴。如果您有很多 SIP 網域，新增主體替代名稱會非常昂貴，您可以設定反向 Proxy，透過使用 HTTP 的連接埠 80 來發行初始自動探索服務要求，而不要透過使用 HTTPS 的連接埠 443 (預設值)。然後要求會重新導向至 Director 或 前端集區上的連接埠 8080。當您在連接埠 80 上發行初始自動探索服務要求時，不需要變更反向 Proxy 的憑證，因為要求是使用 HTTP，而不是 HTTPS。此方法受支援，但不建議使用。

## Internet Information Services (IIS) 需求

建議您針對行動性使用 IIS 7.5、IIS 8.0 或 IIS 8.5。Mobility Service 安裝程式會設定 ASP.NET 中的旗標來增進效能。IIS 7.5 預設會安裝在 Windows Server 2008 R2 上，IIS 8.0 預設會安裝在 Windows Server 2012 上，而 IIS 8.5 則是安裝在 Windows Server 2012 R2 上。Mobility Service 安裝程式會自動變更 ASP.NET 設定。

## 硬體負載平衡器需求

在支援 前端集區的硬體負載平衡器上，必須對於來源設定用於 Web 服務流量的外部 Web 服務虛擬 IP (VIP)。來源相關性有助於確保來自單一用戶端的多個連線會傳送到單一伺服器，以維護工作階段狀態。如需相關性需求的詳細資訊，請參閱＜ [Lync Server 2013 中的負載平衡需求](lync-server-2013-load-balancing-requirements.md)＞。

如果您計劃只透過內部 Wi-Fi 網路來支援 Lync 行動用戶端，則應該要像外部 Web 服務所描述的那樣，針對來源設定內部 Web 服務 VIP。在此情況下，您應該將 source\_addr (或 TCP) 相關性用於硬體負載平衡器上的內部 Web 服務 VIP。如需詳細資訊，請參閱＜ [Lync Server 2013 中的負載平衡需求](lync-server-2013-load-balancing-requirements.md)＞。

## 反向 Proxy 需求

如果您支援 Lync 行動用戶端的自動探索，則需要更新目前的發行規則，如下所示：

  - 如果您決定更新反向 Proxy 憑證上的主體替代名稱清單，並使用 HTTPS 來進行初始自動探索服務要求，則必須為 lyncdiscover.*\<sipdomain\>* 更新 Web 發行規則。一般而言，這會與 前端集區 上外部 Web 服務 URL 的發行規則相結合。

  - 如果您決定使用 HTTP 來進行初始自動探索服務要求，這樣就不需要為反向 Proxy 憑證更新主體替代名稱清單，您必須為連接埠 HTTP/TCP 80 建立新的 Web 發行規則 (如果規則不存在)。如果 HTTP/TCP 80 規則已存在，您可以更新該規則以包含 lyncdiscover.*\<sipdomain\>* 項目。

