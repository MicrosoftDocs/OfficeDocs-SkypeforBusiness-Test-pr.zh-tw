---
title: Revoke-CsSetupPermission
TOCTitle: Revoke-CsSetupPermission
ms:assetid: 3486d164-b1a2-4d4c-9150-cef802674682
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425834(v=OCS.15)
ms:contentKeyID: 49290550
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Revoke-CsSetupPermission

 

_**上次修改主題的時間：** 2015-03-09_

撤銷授與 Active Directory 組織單位 (OU) 的 Lync Server 安裝權限。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Revoke-CsSetupPermission -ComputerOU <String> [-Confirm [<SwitchParameter>]] [-Domain <Fqdn>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會撤銷套用到 litwareinc.com 網域中 CsServers OU 上的安裝權限。

    Revoke-CsSetupPermission -ComputerOU "ou=CsServers,dc=litwareinc,dc=com"

## 詳細描述

安裝 Lync Server 時會進行的網域準備無法自動新增權限，該權限可讓 RTCUniversalServerAdmins 群組成員執行 **Enable-CsTopology** Cmdlet。這代表根據預設，您必須是網域系統管理員才能啟用拓撲。您必須執行 **Grant-CsSetupPermissions** Cmdlet，才能給予 RTCUniversalServerAdmins 群組成員權限以啟用拓樸。此外，您還需要針對每個主控執行 Lync Server 之電腦的 Active Directory 容器執行此 Cmdlet。

使用 **Grant-CsSetupPermission** Cmdlet 所授予的權限可於稍後使用 **Revoke-CsSetupPermission** Cmdlet 移除。如果您執行該 Cmdlet，RTCUniversalServerAdmins 群組將不再擁有指定之 Active Directory 容器的 Lync Server 安裝權限。在這樣的狀況下，您必須具有企業系統管理員或網域系統管理員的身分才能啟用 Lync Server 拓撲。

誰可以執行這個 Cmdlet：您必須具有網域系統管理員身分才能在本機執行 **Revoke-CsSetupPermission** Cmdlet。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Revoke-CsSetupPermission"}

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ComputerOU</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>包含將安裝或已安裝 Lync Server 之電腦帳戶的 OU 辨別名稱 (DN)。例如：-ComputerOU &quot;ou=CsServers,dc=litwareinc,dc=com&quot;。</p>
<p>如果您希望，可在指定 OU 時保持辨別名稱的網域部分關閉。例如：</p>
<p>-ComputerOU &quot;ou=CsServers&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Domain</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>OU 所在網域的名稱。如果未包含此參數，則 <strong>Revoke-CsSetupPermission</strong> Cmdlet 將會尋找目前網域中的 OU。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>當指派原則時所要連絡之網域控制站的完整網域名稱。例如：-DomainController atl-dc-001.litwareinc.com。</p>
<p>若未指定，則當指派原則時 <strong>Revoke-CsSetupPermission</strong> Cmdlet 會與最近的可用網域控制站連絡。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>當指派原則時，所要連絡之通用類別目錄伺服器的完整網域名稱。例如：-GlobalCatalog atl-dc-001.litwareinc.com。</p>
<p>若未指定，則當指派原則時 <strong>Revoke-CsSetupPermission</strong> Cmdlet 會與最近的可用通用類別目錄伺服器連絡。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\OUPermissions.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Revoke-CsSetupPermission** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Grant-CsSetupPermission](grant-cssetuppermission.md)  
[Test-CsSetupPermission](test-cssetuppermission.md)

