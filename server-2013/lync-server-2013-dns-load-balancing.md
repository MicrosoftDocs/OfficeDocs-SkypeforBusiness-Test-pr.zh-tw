---
title: Lync Server 2013 中的 DNS 負載平衡
TOCTitle: Lync Server 2013 中的 DNS 負載平衡
ms:assetid: 7ed0ed20-33ad-4253-926d-21d392590ae7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398634(v=OCS.15)
ms:contentKeyID: 49291456
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 DNS 負載平衡

 

_**上次修改主題的時間：** 2014-01-15_

Lync Server 啟用 DNS 負載平衡，這是一套軟體解決方案，可以明顯減輕在網路上進行負載平衡的管理負荷。DNS 負載平衡可以平衡 Lync Server 所特有的網路流量，例如 SIP 流量和媒體流量。

如果部署 DNS 負載平衡，則組織在硬體負載平衡器方面的管理負荷會低至最低。此外，負載平衡器中針對 SIP 流量的設定錯誤問題所涉及的複雜疑難排解也得以排除。您也可以防止伺服器連線，以便將伺服器離線。DNS 負載平衡也可以確保硬體負載平衡器問題不會影響基本通話路由等這類 SIP 流量元素。

相較於將硬體負載平衡器用於全部的流量類型，如果使用 DNS 負載平衡也能讓您購買成本較低的硬體負載平衡器。您應使用通過 Lync Server 互通性資格測試的負載平衡器。如需負載平衡器互通性測試的詳細資訊，請參閱＜Lync Server 2010 負載平衡器協力廠商＞，網址為：<http://go.microsoft.com/fwlink/?linkid=202452>。

DNS 負載平衡支援前端集區、Edge Server 集區、Director 集區和獨立中繼伺服器集區。

## 前端集區和 Director 集區上的 DNS 負載平衡

您可以針對前端集區和 Director 集區上的 SIP 流量使用 DNS 負載平衡。部署 DNS 負載平衡之後，這些集區還是需要使用硬體負載平衡器，但只限用戶端到伺服器的 HTTPS 流量。硬體負載平衡器會用於用戶端透過連接埠 443 和 80 送出的 HTTPS 流量。

雖然這些集區仍然需要硬體負載平衡器，但是其設定和系統管理主要是針對 HTTPS 流量，這也是硬體負載平衡器的系統管理員比較熟悉的領域。

## DNS 負載平衡以及支援的舊版用戶端和伺服器

DNS 負載平衡只支援對執行 Lync Server 2013 或 Lync Server 2010 的伺服器和 Lync 2013 和 Lync 2010 用戶端進行自動容錯移轉。舊版的用戶端和 Office Communications Server 還是可以連線至執行 DNS 負載平衡的集區，但是如果它們無法連線至 DNS 負載平衡將它們轉介到的第一部伺服器，它們就無法容錯移轉至集區中的另一部伺服器。

此外，如果您在使用 Exchange UM，則只有 Exchange 2010 SP1 或最新的 Service Pack 才具有 Lync Server DNS 負載平衡的支援。如果您使用舊版 Exchange，則下列 Exchange UM 案例沒有容錯移轉功能：

  - 在電話上播放 Enterprise Voice 語音信箱

  - 從 Exchange UM 自動語音應答轉接通話

所有其他 Exchange UM 案例則會正常運作。

## 在前端集區和 Director 集區上部署 DNS 負載平衡

在前端集區和 Director 集區上部署 DNS 負載平衡，需要您對 FQDN 和 DNS 記錄執行一些額外步驟。

  - 集區若要使用 DNS 負載平衡，必須要有兩個 FQDN：一個是供 DNS 負載平衡使用的一般集區 FQDN (如 pool01.contoso.com)，這會解析為集區中伺服器的實體 IP；另一個是集區的 Web 服務的 FQDN (如 web01.contoso.com)，這會解析為集區的虛擬 IP 位址。
    
    在拓撲產生器中，如果您要部署集區的 DNS 負載平衡，則必須在 **\[指定此集區的 Web 服務 URL\]** 頁面中選取 **\[覆寫內部 Web 服務集區 FQDN\]** 核取方塊，並輸入 FQDN，以為集區的 Web 服務建立這個額外的 FQDN。

  - 若要支援 DNS 負載平衡所使用的 FQDN，您必須佈建 DNS，以將集區 FQDN (如 pool01.contoso.com) 解析為集區中所有伺服器的 IP 位址 (例如，192.168.1.1、192.168.1.2 等)。您應該只包含目前部署之伺服器的 IP 位址。
    
    > [!WARNING]
    > 如果您有一個以上的前端集區或前端伺服器，則外部 Web 服務 FQDN 必須是唯一的。例如，如果您將前端伺服器的外部 Web 服務 FQDN 定義為 <strong>pool01.contoso.com</strong>，便無法針對其他的前端集區或前端伺服器使用 <strong>pool01.contoso.com</strong>。如果您同時部署了 Director，則針對任何 Director 或 Director 集區定義的外部 Web 服務 FQDN，在任何其他 Director 或 Director 集區以及任何前端集區或前端伺服器中必須是唯一的。如果決定以自我定義的 FQDN 覆寫內部 Web 服務，各個 FQDN 必須與其他任何前端集區、Director 或 Director 集區各不相同。


## Edge Server 集區上的 DNS 負載平衡

您可以在 Edge Server 集區上部署 DNS 負載平衡。如果這麼做，則必須注意下列考量。

在 Edge Server 上使用 DNS 負載平衡，會導致下列案例喪失容錯移轉能力：

  - 與執行 Lync Server 2010 之前舊版 Office Communications Server 的組織建立同盟。

  - 與公用立即訊息 (IM) 服務 AOL 和 Yahoo\! 的使用者，以及 XMPP 型提供者和伺服器 (如 Google Talk) 的使用者交換立即訊息。
    
    <table>
    <colgroup>
    <col style="width: 100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><ul>
    <li><p>Google Talk 是目前唯一支援的 XMPP 夥伴。</p></li>
    <li><p>自 2012 年 9 月 1 日起，Microsoft Lync 公用 IM 連線使用者訂閱授權 (&quot;PIC USL&quot;) 無法再以新合約或續約的方式購買。持有使用中授權的客戶將可繼續與 Yahoo! Messenger 維持同盟關係直至服務終止日。目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的確切結束日期。如需詳細資訊，請參閱＜<a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>＞。</p></li>
    </ul></td>
    </tr>
    </tbody>
    </table>


只要集區中的所有 Edge Server 都啟動並執行，這些案例就能運作，但是如果其中一個 Edge Server 無法使用，則在這些案例中任何傳送給該 Edge Server 的要求都會失敗，而不是路由至另一個 Edge Server。

如果您正在使用 Exchange UM，必須至少用 Exchange 2013，以支援 Edge 上的 Lync Server DNS 負載平衡。如果您使用舊版 Exchange，您的遠端使用者在下列 Exchange UM 的情況中將無法使用容錯移轉功能：

  - 在電話上播放 Enterprise Voice 語音信箱

  - 從 Exchange UM 自動語音應答轉接通話

所有其他 Exchange UM 案例則會正常運作。

內部 Edge 介面和外部 Edge 介面必須使用相同類型的負載平衡。您不能在一個 Edge 介面上使用 DNS 負載平衡，而在另一個 Edge 介面上使用硬體負載平衡。

## 在 Edge Server 集區上部署 DNS 負載平衡

若要在 Edge Server 集區的外部介面上部署 DNS 負載平衡，您需要下列 DNS 項目：

  - 針對 Access Edge Service，集區中的每部伺服器都需要一個項目。每個項目都必須將 Access Edge Service 的 FQDN (例如，sip.contoso.com) 解析為集區中其中一個 Edge Server 上的 Access Edge Service 的 IP 位址。

  - 針對 Web Conferencing Edge Service，集區中的每部伺服器都需要一個項目。每個項目都必須將 Web Conferencing Edge Service 的 FQDN (例如，webconf.contoso.com) 解析為集區中其中一個 Edge Server 上的 Web Conferencing Edge Service 的 IP 位址。

  - 針 Audio/Video Edge Service，集區中的每部伺服器都需要一個項目。每個項目都必須將 Audio/Video Edge Service 的 FQDN (例如，av.contoso.com) 解析為集區中其中一個 Edge Server 上的 A/V Edge Service 的 IP 位址。

若要在 Edge Server 集區的內部介面上部署 DNS 負載平衡，您必須新增一筆 DNS A 記錄，並讓它將 Edge Server 集區的內部 FQDN 解析為集區中每部伺服器的 IP 位址。

## 在中繼伺服器集區上使用 DNS 負載平衡

您可以在獨立中繼伺服器集區上使用 DNS 負載平衡。所有 SIP 和媒體流量都是透過 DNS 負載平衡進行平衡處理。

若要在中繼伺服器集區上部署 DNS 負載平衡，您必須佈建 DNS，以將集區 FQDN (例如，mediationpool1.contoso.com) 解析為集區中所有伺服器的 IP 位址 (例如，192.168.1.1、192.168.1.2 等)。

## 以 DNS 負載平衡封鎖伺服器的流量

如果您使用 DNS 負載平衡，而您需要封鎖傳輸到特定電腦的流量，僅從 集區 FQDN移除 IP 位址項目並不足夠。您也必須移除電腦的 DNS 項目。

請注意，對於伺服器對伺服器流量，Lync Server 2013 使用拓撲感知的負載平衡。伺服器會讀取中央管理存放區中發行的拓撲，取得拓撲中的伺服器 FQDN，並且在伺服器之間自動散佈流量。若要封鎖伺服器接收伺服器對伺服器流量，您必須從拓撲移除伺服器。

