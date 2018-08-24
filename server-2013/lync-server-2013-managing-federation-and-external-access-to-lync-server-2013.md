---
title: Lync Server 2013：管理 Lync Server 2013 的同盟與外部存取
TOCTitle: 管理 Lync Server 2013 的同盟與外部存取
ms:assetid: 26f806c1-f284-4637-b06b-06270336c540
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520966(v=OCS.15)
ms:contentKeyID: 49290404
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 管理 Lync Server 2013 的同盟與外部存取

 

_**上次修改主題的時間：** 2015-03-09_

支援外部使用者的首要步驟，是部署 Edge Server 或 Edge 集區。如需有關部署 Edge Server 的詳細資訊，請參閱部署文件中的＜ [在 Lync Server 2013 中部署外部使用者存取](lync-server-2013-deploying-external-user-access.md)＞。

在您安裝並設定 Lync Server 2013 的內部部署後，組織中的內部使用者將可與其他在您的 Active Directory 網域服務 (AD DS) 中具有 SIP 帳戶的內部使用者共同作業。共同作業可包含傳送和接收立即訊息，以及會議中目前狀態與參加情況的更新。您可以啟用及設定外部使用者存取，以控制受支援的外部使用者是否可與內部 Lync Server 使用者共同作業。外部使用者可能包含您部署的遠端使用者、同盟使用者 (包括公用立即訊息 (IM) 服務提供者的支援使用者)、XMPP 同盟與會議的匿名參與者。

如果您的部署包含 Lync Server 2013  Edge Server 或 Edge 集區的安裝，則可能的通訊類型範圍會因為外部使用者具有多種存取選擇而大幅擴展，以與其他 SIP 同盟網域的成員、SIP 同盟提供者以及 XMPP 同盟使用者進行通訊。完成 Edge Server 或 Edge 集區的設定後，您要啟用您所要提供的外部使用者存取類型，並設定外部存取的原則。在 Lync Server 2013 中，您可以依工作需求，使用 Lync Server 控制台與 Lync Server 管理命令介面啟用及設定外部使用者存取和原則。如需這些管理工具的詳細資訊，請參閱作業文件中的＜ [Lync Server 2013 系統管理工具](lync-server-2013-lync-server-administrative-tools.md)＞、＜ [Lync Server 管理命令介面](lync-server-2013-lync-server-management-shell.md)＞以及＜ [安裝 Lync Server 2013 系統管理工具](lync-server-2013-install-lync-server-administrative-tools.md)＞。

> [!IMPORTANT]  
> 當您設計外部使用者存取的組態和原則時，必須知道原則的優先順序以及原則的套用方式。 套用到某原則層級的 Lync Server 原則設定，可能會覆寫套用到其他原則層級的設定。Lync Server 原則的優先順序是使用者原則 (影響力最大) 會覆寫網站原則，網站原則則會覆寫全域原則 (影響力最小)。亦即，愈接近原則所影響之物件的原則設定，對物件的影響力愈大。



根據預設，沒有原則是設定為支援外部使用者存取 (包括遠端使用者存取、同盟網域使用者存取)，即使您已為組織啟用外部使用者存取也一樣。若要控制外部使用者存取的使用，您必須設定一個或多個原則，並在每個原則指定支援的外部使用者存取類型。這包括下列外部存取原則：

  - **全域原則**   全域原則是在您部署 Edge Server 時所建立。依預設，全域原則中不會啟用任何外部使用者存取選項。若要在全域層級支援外部使用者存取，您可以設定全域原則來支援一或多個外部使用者存取選項類型。全域原則會套用至組織內所有使用者，但網站原則和使用者原則優先於全域原則。如果刪除全域原則，並不代表將其移除，而是將其重設為預設設定。

  - **網站原則**   您可以建立和設定一或多個網站原則，以對特定網站限制外部使用者存取的支援。網站原則中的設定優先於全域原則，但僅限該網站原則所涵蓋的特定網站。例如，如果您在全域原則中啟用了遠端使用者存取，您可以指定網站原則以對特定網站停用遠端使用者存取。依預設，網站原則會套用至該網站的所有使用者，但您可以將使用者原則指派給個別使用者，以覆寫網站原則設定。

  - **使用者原則**   您可以建立和設定一或多個使用者原則，以對特定使用者限制遠端使用者存取支援。使用者原則中的設定優先於全域與網站原則，但僅限指派該使用者原則的特定使用者。例如，如果您在全域原則和網站原則中啟用了遠端使用者存取，您可以指定使用者原則以停用遠端使用者存取，然後將該使用者原則指派給特定使用者。如果您建立使用者原則，必須將其套用至一或多位使用者，該原則才能生效。

若要決定需要建立或編輯哪些組態設定及原則，請參閱下列決策要點：

**您是否要允許您網域的內部及外部使用者能夠使用立即訊息、Web 會議及音訊/視訊來共同作業？**

依照＜ [在 Lync Server 2013 中設定原則以控制遠端使用者存取](lync-server-2013-configure-policies-to-control-remote-user-access.md)＞及＜ [在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)＞主題中所述進行設定

**您是否要允許匿名使用者加入您部署中使用者所主控的會議，以及收到該會議的邀請？**

依照＜ [在 Lync Server 2013 中指派會議原則以支援匿名使用者](lync-server-2013-assign-conferencing-policies-to-support-anonymous-users.md)＞、＜ [在 Lync Server 2013 中建立或修改會議原則](lync-server-2013-create-or-modify-a-conferencing-policy.md)＞及＜ [Lync Server 2013 中的會議原則設定參考](lync-server-2013-conferencing-policy-settings-reference.md)＞主題中所述進行設定

**您是否要允許使用者與 SIP 同盟網域連絡人進行通訊？**

依照＜ [在 Lync Server 2013 中設定控制同盟使用者存取的原則](lync-server-2013-configure-policies-to-control-federated-user-access.md)＞、＜ [在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)＞及＜ [在 Lync Server 2013 中管理組織的 SIP 同盟網域](lync-server-2013-manage-sip-federated-domains-for-your-organization.md)＞主題中所述進行設定

**若您已啟用與 SIP 同盟網域的通訊，您是否還要啟用與 XMPP 同盟協力廠商連絡人的通訊？**

依照＜ [在 Lync Server 2013 中設定原則以控制 XMPP 同盟使用者存取](lync-server-2013-configure-policies-to-control-xmpp-federated-user-access.md)＞及＜ [在 Lync Server 2013 中管理 XMPP 同盟夥伴](lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md)＞主題中所述進行設定。

**若您已啟用與 SIP 同盟網域的通訊，您是否還要啟用 SIP 同盟自動探索？**

依照＜ [在 Lync Server 2013 中啟用或停用探索同盟協力廠商](lync-server-2013-enable-or-disable-discovery-of-federation-partners.md)＞主題所述進行設定。

**若您已啟用與 SIP 同盟網域的通訊，您是否還要啟用傳送免責聲明給同盟連絡人，以通知他們您使用了封裝功能，且可能會封裝通訊內容？**

依照＜ [在 Lync Server 2013 中啟用或停用傳送封存免責聲明至同盟合作夥伴的功能](lync-server-2013-enable-or-disable-sending-an-archiving-disclaimer-to-federated-partners.md)＞主題所述進行設定。

**您是否要允許使用者與能夠和公用提供者 (例如 Windows Live Messenger、AOL 及 Yahoo\!) 通訊的 SIP 同盟提供者進行通訊？**

依照＜ [在 Lync Server 2013 中設定原則以控制公用使用者存取](lync-server-2013-configure-policies-to-control-public-user-access.md)[在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)＞及＜ [在 Lync Server 2013 中建立或編輯公用 SIP 同盟提供者](lync-server-2013-create-or-edit-public-sip-federated-providers.md)＞主題中所述進行設定。

> [!IMPORTANT]  
> <p>自 2012 年 9 月 1 日起，Microsoft Lync 公用 IM 連線使用者訂閱授權 (&quot;PIC USL&quot;) 無法再以新合約或續約的方式購買。持有使用中授權的客戶將可繼續與 Yahoo! Messenger 維持同盟關係直至服務終止日。目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的結束日期。如需詳細資訊，請參閱 <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>。</p></li>
> <p>PIC USL 是針對每位使用者的每月訂閱授權，為 Lync Server 或 Office Communications Server 與 Yahoo! Messenger 同盟的必要授權。Microsoft 是否提供此項服務視 Yahoo! 的支援而定，而此基礎合約將告結束。</p></li>
> <p>更勝以往，Lync 成為連接全世界組織之間以及個人之間的強大工具。除了 Lync Standard CAL 之外，與 Windows Live Messenger 同盟不需要其他使用者/裝置授權。此清單更將加入 Skype 同盟，讓 Lync 使用者可透過 IM 和語音觸及數億位使用者。</p>


**您是否要允許使用者與執行 Microsoft Office 365、 Microsoft Lync Online 及 Microsoft Lync Online 2010 之裝載提供者的 SIP 同盟提供者進行通訊？**

依照＜ [在 Lync Server 2013 中建立或編輯公用 SIP 同盟提供者](lync-server-2013-create-or-edit-public-sip-federated-providers.md)＞、＜ [在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)＞及＜ [建立或編輯主控的 SIP 同盟提供者 Lync Server 2013](lync-server-2013-create-or-edit-hosted-sip-federated-providers.md)＞主題所述進行設定

**您是否將部署設定在分割 (也稱為混合) 網域中，且該網域的某些使用者在內部部署中具有自己的主伺服器，而其他使用者則是透過線上環境中的主伺服器加以設定？**

依照＜ [在 Lync Server 2013 中設定控制同盟使用者存取的原則](lync-server-2013-configure-policies-to-control-federated-user-access.md)＞、＜ [在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)＞及＜ [建立或編輯主控的 SIP 同盟提供者 Lync Server 2013](lync-server-2013-create-or-edit-hosted-sip-federated-providers.md)＞主題所述進行設定

若您偏好以表格列出需求：


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>同盟存取及外部存取中的索引標籤 (橫向) 同盟存取或外部存取類型 (向下)</th>
<th>外部存取原則</th>
<th>Access Edge 設定</th>
<th>SIP 同盟網域</th>
<th>SIP 同盟提供者</th>
<th>XMPP 同盟協力廠商</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>遠端使用者</p></td>
<td><p><a href="lync-server-2013-configure-policies-to-control-remote-user-access.md">在 Lync Server 2013 中設定原則以控制遠端使用者存取</a></p></td>
<td><p><a href="lync-server-2013-enable-or-disable-remote-user-access.md">在 Lync Server 2013 中啟用或停用遠端使用者存取</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>SIP 同盟連絡人</p></td>
<td><p><a href="lync-server-2013-configure-policies-to-control-federated-user-access.md">在 Lync Server 2013 中設定控制同盟使用者存取的原則</a></p>
<p></p></td>
<td><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線</a></p>
<p><a href="lync-server-2013-enable-or-disable-discovery-of-federation-partners.md">在 Lync Server 2013 中啟用或停用探索同盟協力廠商</a></p>
<p><a href="lync-server-2013-enable-or-disable-sending-an-archiving-disclaimer-to-federated-partners.md">在 Lync Server 2013 中啟用或停用傳送封存免責聲明至同盟合作夥伴的功能</a></p></td>
<td><p><a href="lync-server-2013-manage-sip-federated-domains-for-your-organization.md">在 Lync Server 2013 中管理組織的 SIP 同盟網域</a></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>XMPP 同盟連絡人</p></td>
<td><p><a href="lync-server-2013-configure-policies-to-control-federated-user-access.md">在 Lync Server 2013 中設定控制同盟使用者存取的原則</a></p>
<p><a href="lync-server-2013-configure-policies-to-control-xmpp-federated-user-access.md">在 Lync Server 2013 中設定原則以控制 XMPP 同盟使用者存取</a></p></td>
<td><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p><a href="lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md">在 Lync Server 2013 中管理 XMPP 同盟夥伴</a></p></td>
</tr>
<tr class="even">
<td><p>分割網域 / 混合使用者</p></td>
<td><p><a href="lync-server-2013-configure-policies-to-control-federated-user-access.md">在 Lync Server 2013 中設定控制同盟使用者存取的原則</a></p></td>
<td><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線</a></p></td>
<td><p></p></td>
<td><p><a href="lync-server-2013-create-or-edit-hosted-sip-federated-providers.md">建立或編輯主控的 SIP 同盟提供者 Lync Server 2013</a></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>公用 IM 服務連絡人</p></td>
<td><p><a href="lync-server-2013-configure-policies-to-control-public-user-access.md">在 Lync Server 2013 中設定原則以控制公用使用者存取</a></p></td>
<td><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線</a></p></td>
<td><p></p></td>
<td><p><a href="lync-server-2013-create-or-edit-public-sip-federated-providers.md">在 Lync Server 2013 中建立或編輯公用 SIP 同盟提供者</a></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>匿名使用者對會議的存取權</p></td>
<td><p></p></td>
<td><p><a href="lync-server-2013-assign-conferencing-policies-to-support-anonymous-users.md">在 Lync Server 2013 中指派會議原則以支援匿名使用者</a></p>
<div>

> [!NOTE]  
> 您也必須考慮會議原則的下列組態設定：＜ <a href="lync-server-2013-create-or-modify-a-conferencing-policy.md">在 Lync Server 2013 中建立或修改會議原則</a>＞及＜ <a href="lync-server-2013-conferencing-policy-settings-reference.md">Lync Server 2013 中的會議原則設定參考</a>＞


</div></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


您可以設定外部使用者存取設定，包括任何您要用以控制外部使用者存取的原則，即使您並未啟用組織的外部使用者存取亦然。但只有在您啟用組織的外部使用者存取後，您所設定的原則與其他設定才會生效。當外部使用者存取停用，或未設定外部使用者存取原則加以支援時，外部使用者將無法與您組織的使用者通訊。

Edge 部署會根據您設定 Edge 支援的方式，來驗證外部使用者類型 (除了匿名使用者之外；匿名使用者的驗證，是透過建立會議並邀請參與者時，傳送至匿名參與者的會議識別碼與密碼) 以及控制存取。若要控制通訊，您可以設定一或多項原則並設定其他設定，以定義部署內外之使用者彼此通訊的方式。原則與設定值包含外部使用者存取的預設全域原則，以及您可以建立並設定以針對特定網站或使用者啟用一或多種外部使用者存取類型的網站與使用者原則。

## 本章節內容

  - [在 Lync Server 2013 中管理外部使用存取原則](lync-server-2013-manage-external-access-policy-for-your-organization.md)

  - [在 Lync Server 2013 中管理組織的 Access Edge 設定](lync-server-2013-manage-access-edge-configuration-for-your-organization.md)

  - [在 Lync Server 2013 中管理組織的 SIP 同盟網域](lync-server-2013-manage-sip-federated-domains-for-your-organization.md)

  - [在 Lync Server 2013 中管理組織的 SIP 同盟提供者](lync-server-2013-manage-sip-federated-providers-for-your-organization.md)

  - [在 Lync Server 2013 中管理 XMPP 同盟夥伴](lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md)

  - [為 Lync Online 客戶設定同盟支援](lync-server-2013-configuring-federation-support-for-a-lync-online-customer.md)

