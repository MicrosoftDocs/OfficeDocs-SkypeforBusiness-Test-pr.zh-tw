---
title: Lync Server 2013：在 Lync Server 中會影響 Edge Server 規劃的變更
TOCTitle: 在 Lync Server 2013 中會影響 Edge Server 規劃的變更
ms:assetid: 66305160-c9b8-4bc4-9f24-8ee8d9a294f7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204965(v=OCS.15)
ms:contentKeyID: 49291153
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中會影響 Edge Server 規劃的變更

 

_**上次修改主題的時間：** 2012-10-22_

Lync Server 2013 引進新的功能，為使用者擴充各項功能及通訊方法。 Lync Server 2013 同時也引進對現有服務的變更，讓組織可用的服務獲得更好的整合與延伸。對於可能影響您規劃及部署 Lync Server 2013  Edge Server 服務時的變更，提供摘要如下。

## 支援 IPv6 定址

Lync Server 2013 支援所有 Edge Server 服務的 IPv6 定址。如果已透過 Windows Server 中的組態為介面提供 IPv6 位址，則可透過 拓撲產生器中的 IP 位址組態，在 Edge Server 組態中使用 IPv6 位址。此外，Extensible Messaging and Presence Protocol (XMPP) 亦支援 IPv6，無需外額外的設定。如果拓撲中已設定 IPv6，必要時，XMPP 將會使用 IPv6。

在 Lync Server 2013 中支援 IPv6 的一項新增需求，是針對需要探索並解析為 IPv6 位址的記錄，建立網域名稱系統記錄。IPv6 DNS 使用定義為 **AAAA** 並稱為「四 A」的主機記錄。其他記錄類型則與 IPv4 記錄類型一致。

## 支援 Extensible Messaging and Presence Protocol (XMPP) 部署

Edge Server 引進完全整合的 XMPP Proxy (部署於 Edge Server) 及 XMPP 閘道 (部署於前端伺服器)。您可部署 XMPP 同盟作為選用元件。透過新增及設定 XMPP Proxy 和 XMPP 閘道，可讓 Microsoft Lync 2013 使用者新增以 XMPP 為基礎之協力廠商的連絡人，進行立即訊息 (IM) 和顯示狀態。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Edge Server 中的 XMPP 服務目前僅提供 Lync Server 用戶端及以 XMPP 為基礎的連絡人之間的 IM 和顯示狀態。此外，XMPP 僅裝載在單一網站。</td>
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
<td>Microsoft 已測試過 Lync Server 2013 的 XMPP 功能，確定其可與 Google Talk 建立立即訊息同盟，而 Microsoft 也會負責這項功能的支援工作。對於其他 XMPP 系統，請連絡第三方廠商，確認其系統是否能與 Lync Server 2013 建立同盟，以及其是否有任何部署或疑難排解方面的建議。</td>
</tr>
</tbody>
</table>


## 支援輪流 Audio/Video 驗證及伺服器對伺服器驗證憑證

憑證是用於產生權杖，以核發給 A/V 驗證服務的用戶端與其他取用者，以及用於伺服器對伺服器驗證。Audio/Video 驗證憑證為 *AudioVideoAuthentication* 類型，而伺服器對伺服器驗證憑證為 *OAuthTokenIssuer* 類型。

對於 Audio/Video 驗證，權杖是用於驗證連接埠配置要求，並快取最高可達 8 小時 (權杖的預設存留期)。在一般作業情況下，這是建立並散發驗證資料給 A/V 取用者非常可靠的方法。然而，憑證存留期有限，並且會在預先定義的日期與時間過期 (以建立日期以及建立憑證的憑證授權單位實施的原則為準，此類型的憑證通常為 2 年)。當憑證過期時，由過期憑證建立並由取用者快取的任何權杖，都會失效。只要使用過期憑證建立的權杖都會造成「媒體轉送」配置失敗，而且任何進行中的音訊/視訊工作階段也會失敗。用戶端需要取得由有效憑證建立的新權杖，才能恢復正常的音訊和視訊功能。

伺服器對伺服器驗證由全域憑證管理，並適用於部署中的所有伺服器。該憑證負責驗證 Lync Server 2013 中的伺服器，以及對 Exchange 2013 和 Microsoft SharePoint Server 2013 進行驗證。如需伺服器對伺服器驗證如何運作的詳細資訊，請參閱＜ [在 Lync Server 2013 中管理伺服器對伺服器驗證 (Oauth) 與夥伴應用程式](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md)＞。Audio/Video 驗證程序和伺服器對伺服器驗證程序之間一個非常重要的差別是，驗證的存留期 (或權杖)。對於 Audio/Video 驗證，驗證在 8 小時後過期。伺服器對伺服器驗證則有 24 小時的存留期。您必須針對每個憑證類型加以規劃。

Lync Server 2013 的新功能是能夠在目前的憑證過期之前，籌備好取代的 Audio/Video 驗證憑證和伺服器對伺服器驗證憑證。新的憑證會接著用於產生新的權杖或新的驗證要求，但會保留舊的憑證用於驗證目前的工作階段和驗證。這將幾乎可以有效地完全避免因為權杖和憑證過期造成的失敗。如需此功能及如何設定的詳細資訊，請參閱＜ [於 Set-CsCertificate 使用 -Roll 以預備 Lync Server 2013 中的 AV 與 OAuth 憑證](lync-server-2013-staging-av-and-oauth-certificates-using-roll-in-set-cscertificate.md)＞。

## 降低對 Cookie 為主親和性的依賴

在舊版的 Lync Server 及 Office Communications Server 中，Web 服務會使用 Cookie 為主的親和性，來確保用戶端和 Web 服務工作階段狀態能夠保持。 Lync Server 2013 Web 服務使用內建的親和性機制，消除了大多數對 Cookie 為主親和性的需求。

<table>
<thead>
<tr class="header">
<th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在移轉所有用戶端至即將推出的 Microsoft Lync Mobile 用戶端之前 (發行日期未定)， Microsoft Lync 2010 Mobile 用戶端仍舊必須使用 Cookie 為主的親和性，而且需要設定 Cookie 為主的親和性。</td>
</tr>
</tbody>
</table>


如需 Lync Server 2013 中 Cookie 為主親和性的詳細資訊，請參閱＜ [外部使用者在 Lync Server 2013 中存取時所需的元件](lync-server-2013-components-required-for-external-user-access.md)＞。

## 自動探索增強功能

Lync Server 2013 中的自動探索功能讓用戶端能夠找到通訊可用的其他功能。適用於 Mobility 及 Microsoft Lync 2010 Mobile 的自動探索是在 Lync Server 2010 累計更新：2011 年 11 月中，首次引進 。自動探索功能 (DNS 記錄名稱為 LyncDiscover 和 LyncDiscoverInternal) 讓用戶端可以找到並使用行動性服務 (適用於 Microsoft Lync 2010 Mobile 用戶端)、 Microsoft Lync Web App 以及 Lync Web Scheduler，並且可以與 Microsoft Exchange Server 和 SharePoint Server 進行通訊。在安裝及部署基礎結構和 Lync Server 2013 伺服器時，自動探索一般會安裝做為其中的一部分。 拓撲產生器及 Lync Server 部署精靈消除了原先在 Lync Server 2010 累計更新：2011 年 11 月中所需的大部分組態工作。

## 適用於行動用戶端的服務

由 Lync Server 2010 累計更新：2011 年 11 月引進， Lync Server 2013 中的行動性服務讓執行 Lync Mobile 的行動電話、使用支援的 Apple iOS、Android、Windows Phone 的平板裝置或是 Nokia 行動裝置，都可以執行如傳送和接收立即訊息、檢視連絡人以及檢視顯示狀態等活動。此外，行動裝置也支援部分 企業語音功能，例如按一下以加入會議、從公司撥號、單一號碼連絡、語音信箱以及未接來電通知。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>行動性服務使用前端伺服器中部署的反向 Proxy 和發佈的服務。Edge Server 不需要進行任何變更。最低需求為執行 Lync Server Access Edge Service 之伺服器的輸出 SIP/TCP/5061。</td>
</tr>
</tbody>
</table>


## Director 角色為選用

Lync Server 2013 拓撲中 Director 伺服器的角色並未變更。它仍舊裝載 Web 服務、預先驗證連入使用者要求，以及將外部使用者導向至其主集區。透過將 Director 從建議的角色變更為選用角色，Microsoft 並不是要降低 Director 的價值。目的是在於降低伺服器數量和其他硬體需求 (例如用於 Director 的硬體負載平衡器)，而不犧牲功能和功用。因為 前端伺服器可以執行和 Director 同樣的工作，又不會影響提供的服務，但還是可以選擇部署 Director。您可以放心排除 Director 並確信 前端伺服器會代替 Director 提供相同的服務。

