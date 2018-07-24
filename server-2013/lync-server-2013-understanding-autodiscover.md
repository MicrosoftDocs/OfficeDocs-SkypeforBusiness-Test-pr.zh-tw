---
title: 了解自動探索
TOCTitle: 了解自動探索
ms:assetid: d70a15b7-750b-4e0f-9a7f-0254d6d486c3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945654(v=OCS.15)
ms:contentKeyID: 52056233
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 了解自動探索

 

_**上次修改主題的時間：** 2013-06-03_

Lync Server 2013「自動探索」服務最初是 Microsoft Lync Server 2010 所導入功能，是 Lync Server 2010 2011 年 11 月累計更新的一部分。除了修正，此累計更新也為 Lync Mobile 和 Lync 2013 用戶端提供了支援。

在 Lync Server 2013 中，「自動探索」服務是外部與內部用戶端運作不可或缺的一部分，此外，「自動探索」也延伸到新用戶端，例如最近推出的 Windows 8Lync Windows 市集應用程式。Lync 2013 桌面用戶端也可以使用「自動探索」。在 Lync Server 中，所需的網域名稱系統 (DNS) 記錄 (**lyncdiscover.\<網域\>** 和 **lyncdiscoverinternal.\<網域\>**) 會辨識「自動探索」。此外，更新版本的 Lync 2010 和 Lync 2013 桌面用戶端偏好「自動探索」更甚於網域名稱系統 (DNS) SRV 記錄，只會在 lyncdiscover.\<網域\> 或 lyncdiscoverinternal.\<網域\> 沒有回應或沒有解析的時候使用 DNS SRV 記錄。Windows 8 和 Lync Mobile 的 Lync Windows 市集應用程式 只會使用「自動探索」，而且將不會參照傳統 DNS SRV 記錄。

在 Lync Server 2013 中，「自動探索」擴充為與可向用戶端提供元素、功能及通訊方式的用戶端進行通訊。資訊會透過從用戶端傳送的要求來進行通訊，而 Lync Server Web 服務會以明確定義的回應 (用戶端可使用的名稱，以及如何使用「自動探索回應」文件格式連結這些功能) 予以回應。

了解「自動探索」回應文件最好的方式包括 Web 服務如何透過此文件將功能傳遞給用戶端，仔細分析和定義 Lync Web 服務「自動探索」回應文件典型回應中的每一行。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在後續的詳細資訊中，使用者已經過主伺服器驗證 (回應驗證要求)。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync 自動探索 Web 服務定義於 <strong>Microsoft Developer Network</strong> (MSDN) 程式庫<strong>開放性規格</strong>一節中的 <strong>Microsoft Office 通訊協定</strong>。如需詳細資訊，請參閱完整的規格文件＜Lync 自動探索 Web 服務通訊協定＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=273839" class="uri">http://go.microsoft.com/fwlink/?linkid=273839</a>。如需驗證的詳細資訊，請參閱＜OC 驗證 Web 服務通訊協定＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=279015" class="uri">http://go.microsoft.com/fwlink/?linkid=279015</a>。</td>
</tr>
</tbody>
</table>


## Lync Server Web 服務自動探索回應

當傳送「自動探索」要求時所傳回的回應對於內部或外部用戶端都是相同的，部分可感知定位的參數可能會變更。如果收到用戶端要求，但真實集區不是已連結的集區，則會針對該使用者傳送使用者的主集區。使用者帳戶在不同集區，但是從同一間辦公室登入的同事會收到略為不同的回應。回應會為使用者指示正確的前端伺服器或前端集區。

「自動探索回應」文件範例：

    <AutodiscoverResponse xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" AccessLocation="External">
       <User>
          <SipServerInternalAccess fqdn="pool01.contoso.com" port="5061"/>
          <SipClientInternalAccess fqdn=" pool01.contoso.com" port="443"/>
          <SipServerExternalAccess fqdn="sip.contoso.com" port="5061"/>
          <SipClientExternalAccess fqdn="sip.contoso.com " port="443"/>
          <Link token ="External/Autodiscover" href="https://webexternal.contoso.com/Autodiscover/AutodiscoverService.svc/root"/>
          <Link token="Internal/Autodiscover" href="https://webinternal.contoso.net/Autodiscover/AutodiscoverService.svc/root"/>
          <Link token="External/AuthBroker" href="https://webexternal.contoso.com/Reach/sip.svc"/>
          <Link token="Internal/AuthBroker" href="https://webinternal.contoso.net/Reach/sip.svc"/>
          <Link token="External/WebScheduler" href="https://webexternal.contoso.com/Scheduler"/>
          <Link token="Internal/WebScheduler" href="https://webinternal.contoso.net/Scheduler"/>
          <Link token="External/Mcx" href="https://webexternal.contoso.com/Mcx/McxService.svc"/>
          <Link token="Internal/Mcx" href="https://webexternal.contoso.net/Mcx/McxService.svc"/>
          <Link token="External/Ucwa" href="https://webexternal.contoso.com/ucwa/v1/applications"/>
          <Link token="Internal/Ucwa" href="https://webinternal.contoso.net/ucwa/v1/applications"/>
          <Link token="Ucwa" href="https://webexternal.contoso.com/ucwa/v1/applications"/>
          <Link token="External/XFrame" href="https://webexternal.contoso.com/Autodiscover/XFrame/XFrame.html"/>
          <Link token="Internal/XFrame" href="https://webinternal.contoso.net/Autodiscover/XFrame/XFrame.html"/>
          <Link token="XFrame" href="https://webexternal.contoso.com/Autodiscover/XFrame/XFrame.html"/>
          <Link token="Self" href="https://webexternal.contoso.net/Autodiscover/AutodiscoverService.svc/root/user"/>
       </User>
    </AutodiscoverResponse>

## 自動探索回應文件詳細資訊

「自動探索回應」文件有兩種格式。預設格式為 JavaScript Object Notation (JSON)，另一種格式為可延伸標記語言 (XML) 文件。XML 適用於此範例。要求和回應是可預測的，因為文件已定義可決定格式的架構。文件中描述所使用架構之處位於要求或回應中的第一行：

    <AutodiscoverResponse xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" AccessLocation="External">

**AccessLocation=”External”** 定義表示要求為外部使用者所提出。

  ```
  <SipServerInternalAccess fqdn="pool01.contoso.com" port="5061"/>
  ```
  ```
  <SipServerExternalAccess fqdn="sip.contoso.com" port="5061"/>
  ```

目前不使用 SipServerInternalAccess 和 SipServerExternalAccess。這些項目保留供未來使用。

  ```
  <SipClientInternalAccess fqdn=" pool01.contoso.com" port="443"/>
  ```
  ```
  <SipClientExternalAccess fqdn="sip.contoso.com " port="443"/>
  ```

SipClientInternalAccess 和 SipClientExternalAccess 說明內部或外部用戶端將會用以存取已定義 SIP 伺服器的完整網域名稱和連接埠。Lync 桌面用戶端和 Lync Windows 市集應用程式可使用這些項目，根據其位置 (內部或外部) 尋找 Director 或 前端伺服器。

  ```
  <Link token="Internal/Autodiscover" href="https://webinternal.contoso.net/Autodiscover/AutodiscoverService.svc/root"/>
  ```
  ```
  <Link token ="External/Autodiscover" href="https://webexternal.contoso.com/Autodiscover/AutodiscoverService.svc/root"/>
  ```

`Autodiscover` 參考包含「自動探索」服務的服務進入點。Token 屬性包含服務名稱，而 HREF 是一種 URL，針對可找到服務的用戶端進行定義。外部網路上的用戶端使用 `External/Autodiscover`。「自動探索」服務會安裝成為部署處理程序的一部分，目前不使用 `Internal/Autodiscover`，並加以保留供未來使用。

  ```
  <Link token="Internal/AuthBroker" href="https://webinternal.contoso.net/Reach/sip.svc"/>
  ```
  ```
  <Link token="External/AuthBroker" href="https://webexternal.contoso.com/Reach/sip.svc"/>
  ```

`AuthBroker` 參考包含內部和外部驗證 Broker 服務的服務進入點，在此範例中為 sip.svc。Token 屬性包含服務名稱，HREF 是一種，針對可找到服務的用戶端進行定義。內部網路上的用戶端使用 `Internal/AuthBroker`，外部網路上的用戶端使用 `External/AuthBroker`。AuthBroker 服務會安裝成為內部 Lync Server 2013 部署 Web 服務部署處理程序的一部分。

  ```
  <Link token="Internal/WebScheduler" href="https://webinternal.contoso.net/Scheduler"/>
  ```
  ```
  <Link token="External/WebScheduler" href="https://webexternal.contoso.com/Scheduler"/>
  ```

`WebScheduler` Token 會參照供用戶端存取 Lync Server 會議之 Web 式排程的 URL。目前，僅使用 `External/WebScheduler`。WebScheduler 會於內部 Lync Server 2013 部署 Web 服務部署處理程序中安裝。

  ```
  <Link token="Internal/Mcx" href="https://webexternal.contoso.net/Mcx/McxService.svc"/>
  ```
  ```
  <Link token="External/Mcx" href="https://webexternal.contoso.com/Mcx/McxService.svc"/>
  ```

`Internal/Mcx` 和 `External/Mcx` 是 Mobility Services 的位置，由 Lync Server 2010 累計更新：2011 年 11 月引進。這些參考可繼續用於所有受支援裝置上的 Lync 2010 Mobile。Mcx 服務會安裝成為內部 Lync Server 2013 部署 Web 服務部署處理程序的一部分。

  ```
  <Link token="Internal/Ucwa" href="https://webinternal.contoso.net/ucwa/v1/applications"/>
  ```
  ```
  <Link token="External/Ucwa" href="https://webexternal.contoso.com/ucwa/v1/applications"/>
  ```
  ```
  <Link token="Ucwa" href="https://webexternal.contoso.com/ucwa/v1/applications"/>
  ```

**Internal/Ucwa**、**External/Ucwa** 和 **Ucwa** 為用戶端提供存取整合通訊 Web 應用程式開發介面 (UCWA API，或簡稱為 UCWA) 的方式。`Internal/Ucwa` 和 `External/Ucwa` 虛擬目錄是為日後增強功能所保留的存取點，目前並不使用。可在所有受支援裝置上的 Microsoft Lync Mobile (Lync Server 2013 所引進) 使用 `Ucwa` 虛擬目錄。UCWA 服務會安裝成為內部 Lync Server 2013 部署 Web 服務部署處理程序的一部分。

  ```
  <Link token="Internal/XFrame" href="https://webinternal.contoso.net/Autodiscover/XFrame/XFrame.html"/>
  ```
  ```
  <Link token="External/XFrame" href="https://webexternal.contoso.com/Autodiscover/XFrame/XFrame.html"/>
  ```
  ```
  <Link token="XFrame" href="https://webexternal.contoso.com/Autodiscover/XFrame/XFrame.html"/>
  ```

`Internal/XFrame`、**External/XFrame** 和 **XFrame** 可讓 UCWA 伺服器應用程式進行存取。XFrame 會安裝成為內部 Lync Server 2013 部署 Web 服務部署處理程序的一部分。

    <Link token="Self" href="https://webexternal.contoso.net/Autodiscover/AutodiscoverService.svc/root/user"/>

`Self` Token 涉及提出要求之用戶端 (使用者回應類型) 的特定資訊。提出要求的用戶端來自於外部，而此「自動探索」參考是「自動探索」服務的使用者部分。

## 請參閱

#### 其他資源

[外部使用者為 Lync Server 2013 存取元件的系統需求](lync-server-2013-system-requirements-for-external-user-access-components.md)  
[規劃自動探索](lync-server-2013-planning-for-autodiscover.md)

