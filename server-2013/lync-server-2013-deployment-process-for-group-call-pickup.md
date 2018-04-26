---
title: 群組來電接聽的部署程序
TOCTitle: 群組來電接聽的部署程序
ms:assetid: 082daeac-e667-4e2d-b78d-8e0901f9f0e9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945615(v=OCS.15)
ms:contentKeyID: 52056047
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 群組來電接聽的部署程序

 

_**上次修改主題的時間：** 2015-03-09_

本節將概要說明部署群組來電接聽所需的步驟。您必須先部署具備 企業語音 的 Enterprise Edition 或 Standard Edition，之後才能設定群組來電接聽。在部署 企業語音 時就會安裝並啟用群組來電接聽所需的元件。

### 群組來電接聽部署程序

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
<th>所需群組和角色</th>
<th>部署文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>在拓撲中啟用 SEFAUtil 資源套件工具</p></td>
<td><ol>
<li><p>使用 <strong>New-CsTrustedApplicationPool</strong> Cmdlet 建立新的信任應用程式集區。</p></li>
<li><p>使用 <strong>New-CsTrustedApplication</strong> Cmdlet 指定 SEFAUtil 工具為信任的應用程式。</p></li>
<li><p>執行 <strong>Enable-CsTopology</strong> Cmdlet 啟用拓撲。</p></li>
<li><p>在步驟 1 所建之信任應用程式集區中的 前端伺服器 上安裝 Resource Kit 工具。</p></li>
<li><p>執行 SEFAUtil 來顯示部署中使用者的來電轉接設定，以確認該工具可正確執行。</p></li>
</ol></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-deploy-the-sefautil-tool.md">部署 SEFAUtil 工具</a></p></td>
</tr>
<tr class="even">
<td><p>在通話駐留範圍表中設定電話接聽號碼範圍</p></td>
<td><p>使用 <strong>New-CSCallParkOrbit</strong> Cmdlet 在通話駐留範圍表中建立電話接聽號碼範圍，並且指派電話接聽範圍為 GroupPickup 類型。</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須使用 Lync Server 管理命令介面 才能在通話駐留範圍表中建立、修改、移除及檢視群組來電接聽號碼範圍。Lync Server 控制台 無法使用群組來電接聽號碼範圍。</td>
</tr>
</tbody>
</table>

</div>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>為了能與現有撥號對應表密切整合，號碼範圍通常設定為虛擬分機的區塊。不支援將直接向內撥號 (DID) 號碼指派為通話駐留範圍表中的範圍號碼。</td>
</tr>
</tbody>
</table>

</div></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-configure-call-pickup-group-numbers.md">設定電話接聽群組號碼</a></p></td>
</tr>
<tr class="odd">
<td><p>指派電話接聽號碼給使用者，並且啟用使用者的群組來電接聽</p></td>
<td><p>在 SEFAUtil Resource Kit 工具中使用 /enablegrouppickup 參數，啟用群組來電接聽並指派電話接聽號碼給使用者。</p></td>
<td><p>-</p></td>
<td><p><a href="lync-server-2013-enable-group-call-pickup-for-users-and-assign-a-group-number.md">啟用使用者的群組來電接聽並指派群組號碼</a></p></td>
</tr>
<tr class="even">
<td><p>通知使用者所指派的電話接聽號碼，以及其他任何相關號碼</p></td>
<td><p>因為任何使用者都可以擷取打給群組來電接聽使用者的電話，所以使用者最好不只監控一個群組。</p></td>
<td><p>-</p></td>
<td><p><a href="lync-server-2013-communicate-group-call-pickup-assignment-to-users.md">將群組來電接聽指派傳達給使用者</a></p></td>
</tr>
<tr class="odd">
<td><p>確認群組來電接聽部署</p></td>
<td><p>測試撥打及擷取通話，確保您的設定運作符合預期。</p></td>
<td><p>-</p></td>
<td><p><a href="lync-server-2013-optional-verify-the-group-call-pickup-deployment.md">(選用) 確認群組來電接聽部署</a></p></td>
</tr>
</tbody>
</table>

