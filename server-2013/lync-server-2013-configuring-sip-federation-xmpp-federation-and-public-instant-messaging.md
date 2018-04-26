---
title: Lync Server 2013：設定 SIP 同盟、XMPP 同盟及 Public Instant Messaging
TOCTitle: 設定 SIP 同盟、XMPP 同盟及 Public Instant Messaging
ms:assetid: a6d04f0b-5cb8-4084-a3a2-d501938971f9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205134(v=OCS.15)
ms:contentKeyID: 49291909
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定 SIP 同盟、XMPP 同盟及 Public Instant Messaging

 

_**上次修改主題的時間：** 2015-03-09_

同盟、公用立即訊息連線和 Extensible Messaging and Presence Protocol (XMPP) 定義不同類別的外部使用者 – 同盟使用者。同盟 Lync Server 部署或 XMPP 部署的使用者可存取一組有限的服務，並由外部部署進行驗證。遠端使用者是 Lync Server 部署的成員，可以存取您的部署提供的所有服務。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的確切結束日期。如需詳細資訊，請參閱＜ <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>＞。</td>
</tr>
</tbody>
</table>


公用立即訊息連線是一種特別類型的同盟，可讓 Lync Server 用戶端使用 Lync 2013 存取設定的公用立即訊息合作夥伴。目前的公用立即訊息連線合作夥伴包含：

  -   
    America Online

  -   
    Windows Live

  -   
    Yahoo\!

公用立即訊息連線組態可讓 Lync 使用者透過下列方式存取公用立即訊息連線使用者：

  - IM 和目前狀態

  - Lync 用戶端中公用立即訊息連線使用者連絡人的可見性

  - 與連絡人進行個人對個人的 IM 交談

  - 與 Windows Live 使用者進行音訊和視訊通話

Lync Server 同盟定義 Lync Server 部署與其他 Office Communications Server 2007 R2 或 Lync Server 部署之間的協議。Lync Server 同盟組態可讓 Lync 使用者透過下列方式存取同盟使用者：

  - IM 和目前狀態

  - 在 Lync 用戶端中建立同盟連絡人

XMPP 同盟定義以 eXtensible Messaging and Presence Protocol 為基礎的外部部署。XMPP 組態可讓 Lync 使用者透過下列方式存取允許的 XMPP 網域使用者：

  - IM 和目前狀態 – 僅人員對人員

  - 在 Lync 用戶端中建立 XMPP 同盟連絡人

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


## Edge Server 外部同盟、公用立即訊息連線和 XMPP 使用者部署程序


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>階段</th>
<th>步驟</th>
<th>權限</th>
<th>文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>決定要新增至現有 Edge 部署的選項</p></td>
<td><p>執行 拓撲產生器以編輯 Edge Server 設定、建立並發行拓撲。您現有的邊緣拓撲會將變更從 中央管理存放區複寫到 Edge Server。</p></td>
<td><p>Domain Admins 群組和 RTCUniversalServerAdmins 群組</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以使用本機使用者群組的成員帳戶來編輯拓撲，但發行拓撲需要以 Domain Admins 群組和 RTCUniversalServerAdmins 群組的成員帳戶進行</td>
</tr>
</tbody>
</table>

</div></td>
<td><p><a href="lync-server-2013-building-an-edge-and-director-topology.md">在 Lync Server 2013 中建置 Edge 和 Director 拓撲</a></p></td>
</tr>
<tr class="even">
<td><p>準備進行安裝</p></td>
<td><ol>
<li><p>確定已符合系統先決條件。</p></li>
<li><p>設定內部和外部 DNS 記錄，以支援公用立即訊息連線、Lync 同盟和 XMPP 同盟</p></li>
<li><p>在防火牆設定連接埠和通訊協定，以支援您正在部署的同盟類型</p></li>
<li><p>建立並安裝公用憑證。取得憑證所需的時間，視發出憑證的憑證授權單位 (CA) 而定。這個步驟此時是部署中的選用步驟。如果您此時不執行這個步驟，也必須在 Edge Server 設定期間執行。未取得憑證前，Edge Server Service 無法啟動</p></li>
</ol>
<p></p></td>
<td><p>視組織而定，這些角色通常共享於數個工作群組</p></td>
<td><p><a href="lync-server-2013-planning-for-sip-xmpp-federation-and-public-instant-messaging.md">規劃 Lync Server 2013 中的 SIP、XMPP 同盟和公用立即訊息</a></p></td>
</tr>
<tr class="odd">
<td><p>針對同盟案例設定 Edge Server</p></td>
<td><ol>
<li><p>將匯出的拓撲組態檔傳輸給每部 Edge Server 或允許複寫完成</p></li>
<li><p>重新執行部署精靈以安裝同盟的支援元件</p></li>
<li><p>設定 Edge Server</p></li>
<li><p>為每部 Edge Server 要求並安裝憑證</p></li>
<li><p>重新啟動 Edge Server 服務</p></li>
</ol></td>
<td><p>Administrators 群組</p></td>
<td><p><a href="lync-server-2013-setting-up-lync-federation.md">在 Lync Server 2013 中設定 Lync 同盟</a></p>
<p><a href="lync-server-2013-setting-up-public-instant-messaging-connectivity.md">在 Lync Server 2013 中設定 Public Instant Messaging Connectivity</a></p>
<p><a href="lync-server-2013-setting-up-xmpp-federation.md">在 Lync Server 2013 中設定 XMPP 同盟</a></p></td>
</tr>
<tr class="even">
<td><p>設定外部使用者存取的支援。</p></td>
<td><ol>
<li><p>使用 Lync Server 控制台外部使用者存取</p></li>
<li><p>設定外部存取原則以便與同盟使用者或公用使用者通訊</p></li>
<li><p>設定 SIP 同盟網域以允許或封鎖網域</p></li>
<li><p>啟用公用立即訊息連線提供者的 SIP 同盟提供者</p></li>
<li><p>設定各 XMPP 網域的 XMPP 同盟提供者</p></li>
</ol></td>
<td><p>指派給 CSAdministrator 角色的 RTCUniversalServerAdmins 群組或使用者帳戶</p></td>
<td><p><a href="lync-server-2013-configuring-support-for-external-user-access.md">在 Lync Server 2013 中設定外部使用者存取支援</a></p>
<p><a href="lync-server-2013-configure-media-encryption-for-public-providers.md">在 Lync Server 2013 中設定公用提供者的媒體加密</a></p></td>
</tr>
<tr class="odd">
<td><p>驗證 Edge Server 組態</p></td>
<td><p>驗證伺服器連線以及內部伺服器組態資料的複寫是否正確</p></td>
<td><p>若要驗證複寫，指派給 CSAdministrator 角色的 RTCUniversalServerAdmins 群組或使用者帳戶。若要驗證使用者連線，使用者可作為各類型的同盟使用者</p></td>
<td><p><a href="lync-server-2013-verifying-your-edge-deployment.md">在 Lync Server 2013 中驗證 Edge 部署</a></p>
<p><a href="lync-server-2013-example-xmpp-configuration-–-xmpp-federation-with-google-talk.md">Lync Server 2013 中的範例 XMPP 設定 – XMPP 與 Google Talk 的同盟</a></p></td>
</tr>
</tbody>
</table>

