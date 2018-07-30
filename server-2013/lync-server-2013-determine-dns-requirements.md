---
title: Lync Server 2013：判定 DNS 需求
TOCTitle: 判定 DNS 需求
ms:assetid: 95777017-6282-44c0-a685-f246af0501b4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398758(v=OCS.15)
ms:contentKeyID: 49291712
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Lync Server 2013 判定 DNS 需求

 

_**上次修改主題的時間：** 2015-03-09_

使用下列流程圖來判斷網域名稱系統 (DNS) 需求。Lync Server 2013 累計更新 (2013 年 2 月) 的變更會在適用的地方指明。

> [!IMPORTANT]  
> Microsoft Lync Server 2013 支援使用 IPv6 位址。若要使用 IPv6 位址，您也必須提供對 IPv6 DNS 的支援並設定 DNS 主機 AAAA (稱為「quad-A」) 記錄。在同時使用 IPv4 和 IPv6 的部署中，最好是同時設定和維護 IPv4 及主機 A，並且設定和維護 IPv6 及主機 AAAA。即使您的部署已完全轉換為 IPv6，若外部使用者仍會使用 IPv4，可能仍然需要 IPv4 DNS 主機記錄。



**決定 DNS 需求流程圖**

![DNS 需求流程圖](images/Gg398758.175782ac-363e-408a-912f-8991bf152970(OCS.15).jpg "DNS 需求流程圖")

> [!IMPORTANT]  
> 根據預設，未加入網域之電腦的電腦名稱是主機名稱，而不是完整網域名稱 (FQDN)。拓撲產生器 會使用 FQDN，而不是主機名稱。因此，在要部署為 Edge Server 的電腦 (未加入網域) 名稱中，您必須設定 DNS 尾碼。在指派 Lync Server、Edge Server 及集區的 FQDN 時，<strong>只使用標準字元</strong> (包括 A–Z、a–z、0–9 以及連字號)。請勿使用 Unicode 字元或底線。外部 DNS 和公用 CA (也就是當 FQDN 必須指派至憑證的 SN 時) 通常不支援 FQDN 中的非標準字元。如需其他詳細資訊，請參閱＜<a href="lync-server-2013-configure-dns-host-records.md">為 Lync Server 2013 設定 DNS 主機記錄</a>＞。



## Lync 用戶端如何尋找服務

Microsoft Lync 2010、 Lync 2013 與 Lync Mobile 與用戶端尋找與存取 Lync Server 2013 中服務的方式類似。明顯的例外是使用不同服務位置處理程序的 Lync Windows 市集應用程式。本節詳述用戶端尋找服務的兩種案例，第一種是使用一系列 SRV 與 A 主機記錄的傳統方法，第二種方法僅使用自動探索服務記錄。桌面用戶端的累計更新會從 Lync Server 2010 變更DNS 位置處理程序。對於所有用戶端，會繼續進行 DNS 查詢處理程序，直到傳回成功的查詢為止，或者是可能的 DNS 記錄的清單耗盡，並將最終錯誤傳回用戶端。

對於所有用戶端 ( Lync Windows 市集應用程式 DNS 查閱期間 **除外**) ，會查詢 SRV 記錄，並依照下列順序傳回給用戶端：

1.  lyncdiscoverinternal.*\<domain\>*   內部 Web 服務上自動探索服務的 A (主機) 記錄

2.  lyncdiscover.*\<domain\>*   外部 Web 服務上自動探索服務的 A (主機) 記錄

3.  \_sipinternaltls.\_tcp.*\<domain\>*   用於內部 TLS 連線的 SRV (服務定位器) 記錄

4.  \_sipinternal.\_tcp.*\<domain\>*   用於內部 TCP 連線的 SRV (服務定位器) 記錄 (只有在允許使用 TCP 時才會執行)

5.  \_sip.\_tls.*\<domain\>*   用於外部 TLS 連線的 SRV (服務定位器) 記錄

6.  sipinternal. *\<domain\>*   用於 前端集區 或 Director 的 A (主機) 記錄，只能在內部網路解析

7.  sip.*\<domain\>*   用於內部網路上的 前端集區 或 Director 的 A (主機) 記錄，或當用戶端為外部時，則使用 Access Edge Service

8.  sipexternal.*\<domain\>*   當用戶端為外部時 Access Edge Service 的 A (主機) 記錄

Lync Windows 市集應用程式完全改變處理程序，因為它使用兩筆記錄：

1.  lyncdiscoverinternal.*\<domain\>*   內部 Web 服務上自動探索服務的 A (主機) 記錄

2.  lyncdiscover.*\<domain\>*   外部 Web 服務上自動探索服務的 A (主機) 記錄

沒有其他記錄類型的後援。

新用戶端與舊用戶端所使用之方法相比之下的差異是自動探索服務成為尋找所有服務的首選方法。

連線成功時，自動探索服務會傳回使用者主集區的所有 Web 服務 URL，包括 Mobility Service (稱為 Mcx，針對 IIS 中的服務所建立的虛擬目錄)， Microsoft Lync Web App 及 Web Scheduler URL。不過，內部 Mobility Service URL 及外部 Mobility Service URL 都會與外部 Web 服務 FQDN 相關聯。因此，不論行動裝置在網路內部或外部，裝置一律會通過反向 Proxy 從外部連線至 Mobility Service。

如果已安裝 Lync Server 2013 累計更新 (2013 年 2 月)，則自動探索服務也會將參照傳回內部/UCWA、外部/UCWA，以及 UCWA。這些項目參考 Unified Communications Web API (UCWA) Web 元件。目前，僅會使用項目 UCWA，並提供 Web 元件的 URL 參考。UCWA 是由 Lync 2013 Mobile 用戶端所使用，而非 Lync 2010 Mobile 用戶端所使用之 Mcx Mobility Service。

> [!NOTE]  
> 建立 SRV 記錄時，請切記，這些記錄必須指向建立 DNS SRV 記錄之相同網域中的 DNS A 和 AAAA (如果您使用 IPv6 定址) 記錄。例如，如果 SRV 記錄位於 contoso.com 中，則其指向的 A 和 AAAA (如果您使用 IPv6 定址) 記錄不可位於 fabrikam.com 中。



<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>預設設定是通過外部網站導入行動用戶端流量。您可以修改設定僅傳回內部 URL (如果這樣符合您的需求)。透過此設定，使用者只有在公司網路內部時，才可以在其行動裝置上使用 Lync 行動應用程式。若要定義此設定，請使用 <strong>Set-CsMcxConfiguration</strong> Cmdlet。</td>
</tr>
</tbody>
</table>


> [!NOTE]  
> 雖然行動應用程式也可以連線至其他 Lync Server 2013 服務 (例如通訊錄服務)，但是只有 Mobility Service 的內部行動應用程式 Web 要求才會前往外部 Web FQDN。其他服務要求 (例如通訊錄要求) 不需要此設定。



行動裝置支援手動探索服務。在此情況下，每位使用者必須使用完整的內部和外部自動探索服務 URI (包括通訊協定和路徑) 來設定行動裝置設定，如下所示：

  - https://*\<ExtPoolFQDN\>*/Autodiscover/autodiscoverservice.svc/Root，以進行外部存取

  - https://*\<IntPoolFQDN\>*/AutoDiscover/AutoDiscover.svc/Root，以進行內部存取

建議使用自動探索，而不是手動探索。不過，使用手動設定有助疑難排解行動裝置連線問題。

## 使用 Lync Server 設定 Split-Brain DNS

Split-brain DNS 有數個一般熟知的名稱，例如，split DNS 或 split-horizon DNS。簡單來說，它說明含有兩個 DNS 區域的 DNS 設定，這兩個 DNS 區域具備相同的命名空間，但有一個 DNS 區域僅服務內部要求，而另一個 DNS 區域僅服務外部要求。不過，內部 DNS 中包含的許多 DNS SRV 和 A 記錄將不會包含在外部 DNS 中，反之亦然。如果相同的 DNS 記錄 (例如，www.contoso.com) 同時存在於內部與外部 DNS，則傳回的 IP 位址會根據初始查詢的位置 (內部或外部) 而不同。

> [!IMPORTANT]  
> Split-Brain DNS 目前不支援行動性，具體而言，即為 LyncDiscover 和 LyncDiscoverInternal DNS 記錄。LyncDiscover 必須定義於外部 DNS 伺服器上，而 LyncDiscoverInternal 必須定義於內部 DNS 伺服器上。



就這些主題的目的而言，將使用 split-brain DNS 一詞。

如果您設定 split-brain DNS，下列內部和外部區域包含每個區域中需要的 DNS 記錄類型的摘要。如需詳細資訊，請參閱＜ [Lync Server 2013 中的外部使用者存取案例](lync-server-2013-scenarios-for-external-user-access.md)＞。

**內部 DNS：**

  - 包含名為 contoso.com 的代表性 DNS 區域

  - 內部 contoso.com 區域包含：
    
      - 內部 Lync Server 2013 用戶端自動設定適用的 DNS A 和 AAAA (如果您使用 IPv6 位址) 及 SRV 記錄 (選用)
    
      - Lync Server 2013 Web 服務之自動探索適用的 DNS A 和 AAAA (如果您使用 IPv6 位址) 或 CNAME 記錄 (選用)
    
      - 公司網路中的前端集區名稱、Director 或 Director 集區名稱及所有執行 Lync Server 2013 的內部伺服器適用的 DNS A 和 AAAA (如果您使用 IPv6 位址) 記錄
    
      - 周邊網路中每個 Lync Server 2013 和 Edge Server 的 Edge 內部介面適用的 DNS A 和 AAAA (如果您使用 IPv6 定址) 記錄
    
      - 周邊網路中每個反向 Proxy 伺服器的內部介面適用的 DNS A 和 AAAA (如果您使用 IPv6 位址) 記錄 (選擇地適用於管理反向 Proxy)
    
      - 周邊網路中的所有 Lync Server 2013  Edge Server 內部邊緣介面會使用內部 DNS 區域來解析 contoso.com 的查詢
    
      - 公司網路中所有執行 Lync Server 2013 的伺服器和執行 Lync 2013 的用戶端會指向內部 DNS 伺服器來解析 contoso.com 的查詢，或者在每部 Edge Server 上使用 HOSTS 檔案，以及列出下一個躍點伺服器適用的 A 和 AAAA (如果您使用 IPv6 位址) 記錄，特別是 Director 或 Director VIP、前端集區 VIP 或 Standard Edition Server

**外部 DNS：**

  - 包含名為 contoso.com 的代表性 DNS 區域

  - 外部 contoso.com 區域包含：
    
      - Lync Server 2013 用戶端自動設定適用的 DNS A 和 AAAA (如果您使用 IPv6 位址) 及 SRV 記錄 (選用)
    
      - 可搭配行動性使用的 Lync Server 2013 Web 服務之自動探索適用的 DNS A 和 AAAA (如果您使用 IPv6 位址) 或 CNAME 記錄
    
      - 周邊網路中每個 Lync Server 2013、Edge Server 或硬體負載平衡器虛擬 IP (VIP) 的 Edge 外部介面適用的 DNS A 和 AAAA (如果您使用 IPv6 位址) 及 SRV 記錄
    
      - 周邊網路中反向 Proxy 伺服器的外部介面或反向 Proxy 伺服器集區之 VIP 適用的 DNS A 和 AAAA (如果您使用 IPv6 位址) 記錄

## 不透過 Split-Brain DNS 執行的自動設定

使用 split-brain DNS，只要內部 DNS 區域針對每個使用中的 SIP 網域分別包含一個 \_sipinternaltls.\_tcp SRV 記錄，從內部登入的 Lync Server 2013 使用者就可以使用自動設定功能。不過，如果您不使用 split-brain DNS，除非實作本節稍後說明的其中一個因應措施，否則執行 Lync 之用戶端的內部自動設定就無法運作。這是因為 Lync Server 2013 要求使用者的 SIP URI 必須符合針對自動設定所指定之前端集區的網域。舊版 Communicator 亦同。

例如，如果您有兩個使用中的 SIP 網域，則需要下列 DNS 服務 (SRV) 記錄：

  - 如果使用者以 bob@contoso.com 登入，則下列 SRV 記錄可讓自動設定運作，因為使用者的 SIP 網域 (contoso.com) 符合自動設定前端集區的網域：
    
     \_sipinternaltls.\_tcp.contoso.com. 86400 IN SRV 0 0 5061 pool01.contoso.com

  - 如果使用者以 alice@fabrikam.com 登入，則下列 DNS SRV 記錄可讓第二個 SIP 網域的自動設定運作。
    
     \_sipinternaltls.\_tcp.fabrikam.com. 86400 IN SRV 0 0 5061 pool01.fabrikam.com

基於比較的目的，如果使用者以 tim@litwareinc.com 登入，則下列 DNS SRV 記錄會讓自動設定無法運作，因為用戶端的 SIP 網域 (litwareinc.com) 不符合集區所在的網域 (fabrikam.com)：

 \_sipinternaltls.\_tcp.litwareinc.com. 86400 IN SRV 0 0 5061 pool01.fabrikam.com

如果執行 Lync 的用戶端需要自動設定，請選取下列其中一個選項：

  - **群組原則物件**   使用群組原則物件 (GPO) 來填寫正確的伺服器值。
    
    > [!NOTE]  
    > 此選項不會啟用自動設定，但會自動化手動組態的程序，因此，如果採用此方法，則不需要與自動設定相關聯的 SRV 記錄。
    


  - **相符的內部區域**   在內部 DNS 中建立一個區域來符合外部 DNS 區域 (例如，contoso.com)，並建立與自動設定所使用之 Lync Server 2013 集區對應的 DNS A 和 AAAA (如果您使用 IPv6 位址) 記錄。例如，如果使用者位於 pool01.contoso.net，但以 bob@contoso.com 登入 Lync，請建立名為 contoso.com 的內部 DNS 區域，然後在其中建立 pool01.contoso.com 的 DNS A 和 AAAA (如果您使用 IPv6 位址) 記錄。

  - **精確的內部區域**   如果您無法在內部 DNS 中建立整個區域，可以建立與自動設定所需的 SRV 記錄對應的精確 (亦即專用) 區域，並使用 dnscmd.exe 來填寫這些區域。Dnscmd.exe 是必要的，因為 DNS 使用者介面不支援建立精確區域。例如，如果 SIP 網域是 contoso.com，且您有一個名為 pool01 的前端集區包含兩個前端伺服器，則內部 DNS 中需要下列精確區域和 A 記錄：
    
        dnscmd . /zoneadd _sipinternaltls._tcp.contoso.com. /dsprimary
        dnscmd . /recordadd _sipinternaltls._tcp.contoso.com. @ SRV 0 0 5061 pool01.contoso.com.
        dnscmd . /zoneadd pool01.contoso.com. /dsprimary
        dnscmd . /recordadd pool01.contoso.com. @ A 192.168.10.90
        dnscmd . /recordadd pool01.contoso.com. @ AAAA <IPv6 address>
        dnscmd . /recordadd pool01.contoso.com. @ A 192.168.10.91 
        dnscmd . /recordadd pool01.contoso.com. @ AAAA <IPv6 address>
    
    如果環境包含第二個 SIP 網域 (例如，fabrikam.com)，則內部 DNS 中需要下列精確區域和 A 記錄：
    
        dnscmd . /zoneadd _sipinternaltls._tcp.fabrikam.com. /dsprimary
        dnscmd . /recordadd _sipinternaltls._tcp.fabrikam.com. @ SRV 0 0 5061 pool01.fabrikam.com.
        dnscmd . /zoneadd pool01.fabrikam.com. /dsprimary
        dnscmd . /recordadd pool01.fabrikam.com. @ A 192.168.10.90
        dnscmd . /recordadd pool01.contoso.com. @ AAAA <IPv6 address>
        dnscmd . /recordadd pool01.fabrikam.com. @ A 192.168.10.91
        dnscmd . /recordadd pool01.contoso.com. @ AAAA <IPv6 address>

> [!NOTE]  
> 前端集區 FQDN 出現兩次，但各有不同的 IP 位址。這是因為使用 DNS 負載平衡的關係，如果使用硬體負載平衡，則只會有單一前端集區項目。另外，雖然前端集區 FQDN 值在 contoso.com 範例和 fabrikam.com 範例會有不同，但 IP 位址維持不變。這是因為從這兩個 SIP 網域之一登入的使用者都是以相同的前端集區執行自動設定。



如需詳細資訊，請參閱 DMTF 部落格文章＜Communicator 自動設定和 Split-Brain DNS＞，網址為 <http://go.microsoft.com/fwlink/?linkid=200707>。

> [!NOTE]  
> 每個部落格的內容及其 URL 如有任何變更，恕不另行通知。



## 設定網域名稱系統 (DNS) 以進行災害復原

若要設定 DNS 以將 Lync Server 2013 Web 流量重新導向至您的災害復原和容錯移轉網站，您必須使用 DNS 提供者來支援 GeoDNS。您可以設定適用於 Web 的 DNS 記錄來支援災害復原，如此，即使有一整個 前端集區失效，使用 Web 服務的功能還是能夠繼續執行。此災害復原功能支援自動探索 (Lyncdiscover URL)、會議與撥入簡單 URL。

您可以在 GeoDNS 提供者上定義和設定 Web 服務之內部與外部解析適用的其他 DNS 主機 (A 和 AAAA (如果使用 IPv6)) 記錄。下列詳細資料假設成對的集區、分散在各地，以及您的提供者可能會利用循環配置資源 DNS 來支援的 GeoDNS，或者設定為將集區1 當成主要集區來使用，以及在發生通訊遺失或硬體失敗時容錯移轉至集區2。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>GeoDNS 記錄 (範例)</th>
<th>集區記錄 (範例)</th>
<th>CNAME 記錄 (範例)</th>
<th>DNS 設定 (選取一個選項)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Meet-int.geolb.contoso.com</p></td>
<td><p>Pool1InternalWebFQDN.contoso.com</p>
<p>Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Meet.contoso.com 別名為 Pool1InternalWebFQDN.contoso.com</p>
<p>Meet.contoso.com 別名為 Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>集區間的循環配置資源</p>
<p>使用主要，如果失敗則連線到次要</p></td>
</tr>
<tr class="even">
<td><p>Meet-ext.geolb.contoso.com</p></td>
<td><p>Pool1ExternalWebFQDN.contoso.com</p>
<p>Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Meet.contoso.com 別名為 Pool1ExternalWebFQDN.contoso.com</p>
<p>Meet.contoso.com 別名為 Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>集區間的循環配置資源</p>
<p>使用主要，如果失敗則連線到次要</p></td>
</tr>
<tr class="odd">
<td><p>Dialin-int.geolb.contoso.com</p></td>
<td><p>Pool1InternalWebFQDN.contoso.com</p>
<p>Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Dialin.contoso.com 別名為 Pool1InternalWebFQDN.contoso.com</p>
<p>Dialin.contoso.com 別名為 Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>集區間的循環配置資源</p>
<p>使用主要，如果失敗則連線到次要</p></td>
</tr>
<tr class="even">
<td><p>Dialin-ext.geolb.contoso.com</p></td>
<td><p>Pool1ExternalWebFQDN.contoso.com</p>
<p>Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Dialin.contoso.com 別名為 Pool1ExternalWebFQDN.contoso.com</p>
<p>Dialin.contoso.com 別名為 Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>集區間的循環配置資源</p>
<p>使用主要，如果失敗則連線到次要</p></td>
</tr>
<tr class="odd">
<td><p>Lyncdiscoverint-int.geolb.contoso.com</p></td>
<td><p>Pool1InternalWebFQDN.contoso.com</p>
<p>Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Lyncdiscoverinternal.contoso.com 別名為 Pool1InternalWebFQDN.contoso.com</p>
<p>Lyncdiscoverinternal.contoso.com 別名為 Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>集區間的循環配置資源</p>
<p>使用主要，如果失敗則連線到次要</p></td>
</tr>
<tr class="even">
<td><p>Lyncdiscover-ext.geolb.contoso.com</p></td>
<td><p>Pool1ExternalWebFQDN.contoso.com</p>
<p>Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Lyncdiscover.contoso.com 別名為 Pool1ExternalWebFQDN.contoso.com</p>
<p>Lyncdiscover.contoso.com 別名為 Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>集區間的循環配置資源</p>
<p>使用主要，如果失敗則連線到次要</p></td>
</tr>
<tr class="odd">
<td><p>Scheduler-int.geolb.contoso.com</p></td>
<td><p>Pool1InternalWebFQDN.contoso.com</p>
<p>Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Scheduler.contoso.com 別名為 Pool1InternalWebFQDN.contoso.com</p>
<p>Scheduler.contoso.com 別名為 Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>集區間的循環配置資源</p>
<p>使用主要，如果失敗則連線到次要</p></td>
</tr>
<tr class="even">
<td><p>Scheduler-ext.geolb.contoso.com</p></td>
<td><p>Pool1ExternalWebFQDN.contoso.com</p>
<p>Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Scheduler.contoso.com 別名為 Pool1ExternalWebFQDN.contoso.com</p>
<p>Scheduler.contoso.com 別名為 Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>集區間的循環配置資源</p>
<p>使用主要，如果失敗則連線到次要</p></td>
</tr>
</tbody>
</table>


## DNS 負載平衡

DNS 負載平衡通常是在應用程式層級實作。應用程式 (例如，執行 Lync 的用戶端) 在進行集區完整網域名稱 (FQDN) 的 DNS A 和 AAAA (如果您使用 IPv6 位址) 記錄查詢後，會嘗試以所得到的其中一個 IP 位址連線至集區中的某部伺服器。

例如，如果名為 pool01.contoso.com 的集區中有三個前端伺服器，則會發生下列情形：

  - 執行 Lync 的用戶端向 DNS 查詢 pool01.contoso.com。此查詢會傳回如下的三個 IP 位址並將之放入快取 (順序不一定)：
    
    pool01.contoso.com      192.168.10.90
    
    pool01.contoso.com      192.168.10.91
    
    pool01.contoso.com      192.168.10.92

  - 用戶端嘗試對其中一個 IP 位址建立傳輸控制通訊協定 (TCP) 連線。如果失敗，則用戶端會嘗試使用快取中的下一個 IP 位址。

  - 如果 TCP 連線成功，用戶端便會交涉 TLS 來連線至 pool01.contoso.com 上的主要登錄器。

  - 如果用戶端在嘗試所有快取的項目之後無法成功連線，就會向使用者通知目前沒有執行 Lync Server 2013 的伺服器可用。

> [!NOTE]  
> DNS 負載平衡不同於 DNS 循環配置資源 (DNS RR)，後者通常是指依賴 DNS 提供不同順序的 IP 位址 (與集區中的伺服器對應) 來進行的負載平衡。DNS RR 通常只允許負載分散，而不允許容錯移轉。例如，如果連線至由 DNS A 和 AAAA (如果您使用 IPv6 位址) 查詢所傳回的某一個 IP 位址失敗，則連線即會失敗。因此，DNS 循環配置資源本身比 DNS 負載平衡更不可靠。您可以搭配使用 DNS 循環配置資源和 DNS 負載平衡。



DNS 負載平衡適合用於：

  - 伺服器對伺服器的 SIP 到 Edge Server 的負載平衡

  - 整合通訊應用程式服務 (UCAS) 應用程式 (例如會議自動語音應答、回應群組和通話駐留) 的負載平衡

  - 防止對 UCAS 應用程式建立新連線 (又稱為「清空」)

  - 用戶端與 Edge Server 之間所有用戶端對伺服器的流量的負載平衡

DNS 負載平衡不適合用於：

  - 用戶端對伺服器的網頁流量到 Director 或前端伺服器

DNS 負載平衡和同盟流量：

如果 DNS SRV 查詢傳回多個 DNS 記錄，Access Edge Service 一律會挑選數字優先順序最低且數字加權最高的 DNS SRV 記錄。「網際網路工程任務推動小組」文件＜指定服務位置 (DNS SRV) 的 DNS RR＞ <http://www.ietf.org/rfc/rfc2782.txt> 指定如果有多個已定義的 DNS SRV 記錄，會先依優先順序使用，然後是加權。例如，DNS SRV 記錄 A 的權重是 20，優先順序是 40，而 DNS SRV 記錄 B 的權重是 10，優先順序是 50。將選取帶有優先順序 40 的 DNS SRV 記錄 A。以下規則適用於 DNS SRV 記錄選擇：

  - 優先順序是優先考量。用戶端「必須」嘗試連線由具有可達最低數字優先順序之 DNS SRV 記錄所定義的目標主機。具有相同優先順序的目標「應該」以加權欄位中定義的順序來嘗試。

  - 加權欄位可指定帶有相同優先順序之項目的相對加權。較高的加權按比例「應該」提供較高的選取可能性。未進行任何伺服器選擇時，DNS 管理員「應該」使用加權 0。如果有加權大於 0 的記錄存在，則加權 0 的記錄的選取機會應該比較小。

如果傳回多個具有具有相同優先順序及加權的 DNS SRV 查詢，Access Edge Service 將選取最先從 DNS 伺服器中收到的 SRV 記錄。

