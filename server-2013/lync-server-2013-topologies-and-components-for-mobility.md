---
title: Lync Server 2013：行動性的拓撲和元件
TOCTitle: 行動性的拓撲和元件
ms:assetid: be3cae7a-095d-4785-91ba-6fac99eba92a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690037(v=OCS.15)
ms:contentKeyID: 49292159
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的行動性的拓撲和元件

 

_**上次修改主題的時間：** 2013-02-17_

    The information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.

為了支援行動裝置上的 Lync 行動應用程式，Lync Server 2013 提供三項服務：Lync Server 2013 Mcx Mobility Service、Lync Server 2013 自動探索服務及 Lync Server 2013 推播通知服務。Lync Server 2013 累計更新 (2013 年 2 月) 為 Lync 2013 Mobile 用戶端新增免費但卻進階的服務：透過使用整合通訊 Web API 或 UCWA 而取得行動支援。本節簡要說明這些元件並識別支援行動性的 Lync Server 2013 拓撲。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>行動服務也能用於混合部署。如果使用者是在家上網，您不需要部署服務就能支援行動性。但您需要定義「自動探索服務」的設定，好讓使用者尋找其線上身分識別。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您要規劃外部使用者連線 (例如同盟、外部使用者存取或行動性功能)，則須使用 Edge Server 搭配 Standard Edition 伺服器 和 前端伺服器或 前端集區。 Standard Edition 伺服器 和 前端伺服器或 前端集區沒有可供外部使用者存取您內部部署的必要元件，或是供內部部署與外部使用者通訊的必要元件。如需包含外部使用者與內部使用者共同作業或通訊的所有案例，包括行動性，您必須至少部署一部 Edge Server 和一個反向 Proxy。<br />
「推播通知」 使用 Lync Online 服務的一種同盟，用於裝載「推播通知結算所」(PNCH)。當行動裝置處於非使用的狀態時，推播通知會參考音效通知、螢幕上通知 (文字) 和徽章，這些項目由應用程式向 Apple iPhone、iPad 和 Windows Phone 進行推播。PNCH 會從 Lync Server 收到推播通知。當 PNCH 收到訊息通知後，PNCH 會根據訊息的預期行動用戶端收件者，透過 Apple 推播通知服務或 Lync Server 2013 推播通知服務，將通知轉寄給行動用戶端。PNCH 對這些行動用戶端而言，是必要服務。為了與 Lync Online 同盟，PNCH 使用 Edge Server 和憑證確保機密性和驗證、原則以及正確設定的網域名稱系統 (DNS) 記錄。Nokia Symbian 和 Android 型 Lync Mobile 用戶端不使用 PNCH。如需規劃和部署 Edge Server 的詳細資訊，請參閱＜ <a href="lync-server-2013-planning-for-external-user-access.md">在 Lync Server 2013 中規劃外部使用者存取</a>＞和＜ <a href="lync-server-2013-deploying-external-user-access.md">在 Lync Server 2013 中部署外部使用者存取</a>＞。<br />
使用 Apple 裝置的 Lync 2013 Mobile 用戶端引進了 Lync Server 2013 累計更新 (2013 年 2 月)，不再使用推播通知或推播通知結算所 (PNCH)。 Windows Phone 上的 Lync 2013 Mobile 用戶端仍使用推播通知和 PNCH。</td>
</tr>
</tbody>
</table>


## 行動性元件

支援行動性的服務如下：

  - **Lync Server 2013 整合通訊 Web API (UCWA)** 提供在 Lync Server 2013 中與行動和 Web 用戶端即時通訊的服務。將 Lync Server 2013 累計更新 (2013 年 2 月) 部署至 前端伺服器和 Director時，該安裝會在內部和外部 Web 服務 (Ucwa) 建立虛擬目錄。屬於 Ucwa 虛擬目錄的 Web 元件會接受來自於啟用 UCWA 之用戶端的來電。用戶端應用程式透過 REST 介面進行目前狀態、聯絡人、立即訊息、VoIP、視訊會議，以及共同作業等通訊。UCWA 使用 P-GET 型通道傳送事件，例如來電、立即訊息或用戶端應用程式的訊息。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>REST 或具體狀態傳輸是一種軟體架構型式，用於許多表單所廣泛採用的分散式系統，非常適合一般 Web 服務的需求。</td>
    </tr>
    </tbody>
    </table>


  - **Lync Server 2013 Mobility Service (Mcx)** 此項服務可支援在行動裝置上使用 Lync 功能，例如立即訊息 (IM)、目前狀態及聯絡人。Mobility Service 安裝在每個集區中的每一部 前端伺服器上，以支援行動裝置上的 Lync 功能。安裝 Lync Server 2013 的時候，會同時在 前端伺服器內部網站和外部網站下建立新的虛擬目錄 (Mcx)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>具備 Lync Server 2013 累計更新 (2013 年 2 月) 的 Lync Server 2013 可同時支援 Lync Server 2010 累計更新 (November 2011 年 11 月) 所引進的 Mobility Service (通常稱為 Mcx) 以及 UCWA Web 元件。這兩項行動性服務的組合可讓使用 Lync 2010 Mobile 的使用者和 Lync Server 2013 上的 Lync 2013 Mobile 用戶端進行互通性的使用。</td>
    </tr>
    </tbody>
    </table>


  - **Lync Server 2013 自動探索服務**   此服務會識別使用者的位置，並允許行動裝置和其他 Lync 用戶端尋找資源，例如 Lync Server 2013 Web 服務的內部和外部 URL，以及 Mcx 或 UCWA 的 URL，而不論網路位置為何。自動探索使用硬式編碼主機名稱 (若是網路內部的使用者，則為 lyncdiscoverinternal；若是網路外部的使用者，則為 lyncdiscover)，以及使用者的 SIP 網域，並支援使用 HTTP 或 HTTPS 的用戶端連線。
    
    自動探索服務會安裝在每一部 前端伺服器和每個集區中的每一部 Director 上，以在行動裝置上支援 Lync 功能。每當您安裝自動探索服務時，會同時在 前端伺服器和 Director 上的內部網站和外部網站下建立新的虛擬目錄 (Autodiscover)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>自動探索服務會列於此處是因為在提供行動用戶端服務時它會保持重要的元件。 Lync Server 2013 中的自動探索角色已擴充為可為所有用戶端提供服務。如需自動探索服務規劃的詳細資訊，請參閱＜ <a href="lync-server-2013-planning-for-autodiscover.md">規劃自動探索</a>＞。</td>
    </tr>
    </tbody>
    </table>


  - **推播通知服務**   此服務是位於 Lync Online 資料中心的雲端架構服務。當支援的 Apple iOS 裝置或 Windows Phone 上的 Lync 行動應用程式非作用中時，由於這些裝置不支援行動應用程式在背景執行，因此將無法回應新事件 (例如新的立即訊息 (IM) 邀請、未接的立即訊息、未接來電或語音信箱)。在這些情況下，會將新事件的通知 (稱為「推播通知」) 傳送至行動裝置。行動服務會將通知傳送至雲端架構的推播通知服務，該服務接著會將通知傳送至 Apple 推播通知服務 (APNS) (適用於支援的 Apple iOS 裝置) 或 Microsoft 推播通知服務 (MPNS) (適用於 Windows Phone)，再由這些服務將通知傳送至行動裝置。使用者接著可以回應行動裝置上的通知來啟動應用程式。
    
    Apple 和 Windows Phone 裝置上的 Lync 2010 Mobile 使用推播通知。Apple 裝置的 Lync 2013 Mobile 用戶端引進了 Lync Server 2013 累計更新 (2013 年 2 月)，不再使用推播通知或推播通知結算所 (PNCH)。

下圖說明推播通知服務如何與使用 UCWA 和 Lync 2013 Mobile 用戶端的 Lync Server 2013 拓撲整合。

![推播通知服務 UCWA](images/Hh690037.166d60fd-ff71-4ffe-9f66-3c8bbde0b5ae(OCS.15).jpg "推播通知服務 UCWA")

Lync Server 2010 引進的累計更新 (2011 年 11 月)，該 Mcx 服務為 Lync 2010 Mobile 用戶端提供服務。下圖說明使用 Mcx 和 Lync 2010 Mobile 用戶端套用至拓撲的「推播通知服務」。

![推播通知服務 MCX](images/Hh690037.3081634e-60e7-4348-b24e-bbbf05a90f5f(OCS.15).jpg "推播通知服務 MCX")

## 支援的拓撲

套用 Lync Server 2013 累計更新 (2013 年 2 月) 新增 UCWA Web 元件以支援下列拓撲中 Lync 2013 Mobile 用戶端功能的行動性：

  - Lync Server 2013  Standard Edition

  - Lync Server 2013 Enterprise Edition

Edge Server 可以是 Lync Server 2010Edge Server。

沒有 Lync Server 2013 累計更新的 Lync Server 2013 部署 (2013 年 2 月) 會使用 Mcx Mobility Service 並可提供僅適用於 Lync 2010 Mobile 的服務。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用兩個網路介面與 中繼伺服器角色組合的 前端伺服器可支援 Mobility Service，但是您必須採取適當的步驟設定介面。您必須將 IP 位址指派至特定介面，該介面會做為 中繼伺服器進行通訊，網路介面 IP 會做為 前端伺服器進行通訊。您可在 拓撲產生器執行此項作業，方法是針對每項服務選取正確的 IP 位址，而非使用預設 <strong>使用所有設定的 IP 位址</strong>。</td>
</tr>
</tbody>
</table>


## 請參閱

#### 其他資源

[在 Lync Server 2013 中規劃外部使用者存取](lync-server-2013-planning-for-external-user-access.md)  
[在 Lync Server 2013 中部署外部使用者存取](lync-server-2013-deploying-external-user-access.md)  
[規劃自動探索](lync-server-2013-planning-for-autodiscover.md)

