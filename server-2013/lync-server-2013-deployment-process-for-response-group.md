---
title: Lync Server 2013：回應群組部署程序
TOCTitle: 回應群組部署程序
ms:assetid: d390c8a1-dc6e-44d8-b386-2be1fca9877c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205270(v=OCS.15)
ms:contentKeyID: 49292430
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的回應群組部署程序

 

_**上次修改主題的時間：** 2015-03-09_

本節將概要說明部署 回應群組應用程式所需的階段與步驟。

### 回應群組部署程序

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
<th>部署文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>安裝 回應群組應用程式</p></td>
<td><p>當您部署 企業語音時，預設會安裝及啟動 回應群組應用程式。</p></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-deploying-enterprise-voice.md">在 Lync Server 2013 中部署企業語音</a></p></td>
</tr>
<tr class="even">
<td><p>安裝 回應群組的元件</p></td>
<td><p>Lync Server Cmdlet、 Lync Server 控制台、 回應群組設定工具、代理人的登入與登出主控台以及回應群組用戶端 Web 服務。當您部署 Enterprise Edition 集區或 Standard Edition 伺服器時，就會安裝 Web 服務。</p></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-deploying-lync-server.md">部署 Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>啟用 Lync 2013 與 企業語音的使用者</p></td>
<td><p>啟用即將成為 Lync Server 與 企業語音代理人的使用者。您必須先啟用使用者，才能將他們新增至代理人群組。一般而言， Lync Server 是在 Enterprise Edition 或 Standard Edition 伺服器 部署期間啟用使用者。 企業語音則是在 企業語音部署期間啟用使用者。</p></td>
<td><p>RTCUniversalUserAdmins</p>
<p>CsUserAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-disable-or-re-enable-user-account-for-lync-server.md">停用或重新啟用 Lync Server 的使用者帳戶</a></p>
<p><a href="lync-server-2013-enable-users-for-enterprise-voice.md">在 Lync Server 2013 中為使用者啟用企業語音</a></p></td>
</tr>
<tr class="even">
<td><p>建立和設定回應群組，其中包含代理人群組、佇列及工作流程</p></td>
<td><ol>
<li><p>使用 Lync Server 控制台或 Lync Server 管理命令介面執行下列動作：</p>
<ol>
<li><p>建立和設定代理人群組。</p></li>
<li><p>建立和設定佇列。</p></li>
</ol></li>
<li><p>您可以選擇性使用 Lync Server 管理命令介面來建立預先定義的回應群組營業時間與假日。</p></li>
<li><p>使用 回應群組設定工具或 Lync Server 管理命令介面來建立工作流程 (群組搜尋或互動語音回應 (IVR) 通話流程)，包括自訂的回應群組營業時間與假日。</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以透過 Lync Server 控制台來存取 回應群組設定工具。</td>
</tr>
</tbody>
</table>

</div></li>
</ol></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p>
<p>CsResponseGroupManager</p></td>
<td><p><a href="lync-server-2013-create-response-group-agent-groups.md">在 Lync Server 2013 中建立回應群組代理群組</a></p>
<p><a href="lync-server-2013-create-response-group-queues.md">在 Lync Server 2013 中建立回應群組佇列</a></p>
<p><a href="lync-server-2013-optional-define-response-group-business-hours.md">(選用) 在 Lync Server 2013 中定義回應群組營業時間</a></p>
<p><a href="lync-server-2013-optional-define-response-group-holiday-sets.md">(選用) 在 Lync Server 2013 中定義回應群組假日集</a></p>
<p><a href="lync-server-2013-create-or-modify-a-workflow.md">在 Lync Server 2013 中建立或修改工作流程</a></p></td>
</tr>
<tr class="odd">
<td><p>(選用) 自訂應用程式層級設定</p></td>
<td><p>使用 Lync Server 管理命令介面自訂預設的等候音樂設定、預設的等候音樂音訊檔案、代理人回電寬限期以及來電內容設定。</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-managing-application-level-response-group-settings.md">在 Lync Server 2013 中管理應用程式層級回應群組設定</a></p></td>
</tr>
<tr class="even">
<td><p>(選用) 委派管理回應群組</p></td>
<td><p>將 CsResponseGroupManager 角色指派給使用者，以委派回應群組的設定。接著， 回應群組管理員可以設定要指派的回應群組。</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-planning-for-role-based-access-control.md">在 Lync Server 2013 中規劃角色型存取控制</a></p></td>
</tr>
<tr class="odd">
<td><p>確認回應群組部署</p></td>
<td><p>測試接聽群組搜尋或互動語音回應系統工作流程的電話，以確認您的設定如預期般運作。</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
</tr>
</tbody>
</table>

