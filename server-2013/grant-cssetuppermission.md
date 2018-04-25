---
title: Grant-CsSetupPermission
TOCTitle: Grant-CsSetupPermission
ms:assetid: 753bccc1-edb4-48c9-bd0a-2db5d86f8c5e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398569(v=OCS.15)
ms:contentKeyID: 49291352
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsSetupPermission

 

_**上次修改主題的時間：** 2015-03-09_

授與 Active Directory 組織單位 (OU) 上之 Lync Server 的設定權限。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Grant-CsSetupPermission -ComputerOU <String> [-Confirm [<SwitchParameter>]] [-Domain <Fqdn>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會在網域 litwareinc.com 內授與 CsServers OU 的安裝權限。

    Grant-CsSetupPermission -ComputerOU "ou=CsServers,dc=litwareinc,dc=com"

## 詳細描述

安裝 Lync Server 時會進行的網域準備無法自動新增權限，該權限可讓 RTCUniversalServerAdmins 群組成員執行 **Enable-CsTopology** Cmdlet。這代表根據預設，您必須為網域系統管理員才能啟用拓樸。您必須執行 **Grant-CsSetupPermissions** Cmdlet，才能給予 RTCUniversalServerAdmins 群組成員權限以啟用拓樸。此外，您必須針對裝載執行 Lync Server 之電腦的每個 Active Directory 容器，執行此 Cmdlet。

請記住，這個 Cmdlet 只會將權限授與 RTCUniversalServerAdmins 群組；您無法使用這個 Cmdlet 將權限授與其他安全性群組或個別使用者。

誰可以執行這個 Cmdlet：您必須是網域系統管理員才能在本機執行 **Grant-CsSetupPermission** Cmdlet。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsSetupPermission"}

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
<td><p>包含將安裝或已安裝 Lync Server 之電腦帳戶的 OU 辨別名稱。例如：&quot;ou=CsServers,dc=litwareinc,dc=com&quot;。</p>
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
<td><p>OU 所在網域的名稱。如果未包含此參數，<strong>Grant-CsSetupPermission</strong> Cmdlet 將在目前的網域尋找 OU。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>當指派原則時所要連絡之網域控制站的完整網域名稱。例如：-DomainController atl-dc-001.litwareinc.com。</p>
<p>若未指定，則當指派原則時 <strong>Grant-CsSetupPermission</strong> Cmdlet 會與最近的可用網域控制站連絡。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>當指派原則時，所要連絡之通用類別目錄伺服器的完整網域名稱。例如：-GlobalCatalog atl-dc-001.litwareinc.com。</p>
<p>若未指定，則當指派原則時 <strong>Grant-CsSetupPermission</strong> Cmdlet 會與最近的可用通用類別目錄伺服器連絡。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\SetupPermissions.html&quot;</p></td>
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

無。**Grant-CsSetupPermission** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。**Grant-CsSetupPermission** Cmdlet 不會傳回任何物件或值。

## 請參閱

#### 其他資源

[Revoke-CsSetupPermission](revoke-cssetuppermission.md)  
[Test-CsSetupPermission](test-cssetuppermission.md)

