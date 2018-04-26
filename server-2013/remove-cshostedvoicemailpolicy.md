---
title: Remove-CsHostedVoicemailPolicy
TOCTitle: Remove-CsHostedVoicemailPolicy
ms:assetid: 13968bbe-1403-46de-b02a-ed61e712d1b3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398211(v=OCS.15)
ms:contentKeyID: 49290162
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsHostedVoicemailPolicy

 

_**上次修改主題的時間：** 2015-03-09_

移除代管的語音信箱原則。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsHostedVoicemailPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此命令會移除 ExRedmond 個別使用者原則的代管語音信箱原則。

    Remove-CsHostedVoicemailPolicy -Identity ExRedmond

## 範例 2

範例 2 中的命令會移除所有個別使用者的託管語音信箱原則。命令一開始會先呼叫 **Get-CsHostedVoicemailPolicy** Cmdlet 搭配 Filter "tag\*"，以擷取定義為個別使用者原則的所有原則。然後再將該原則集合管線傳送到 **Remove-CsHostedVoicemailPolicy** Cmdlet，以刪除每個原則。

    Get-CsHostedVoicemailPolicy -Filter tag* | Remove-CsHostedVoicemailPolicy

## 詳細描述

此 Cmdlet 會移除原則，這個原則會指定如何將使用者未接聽的來電轉接至託管的 Exchange 整合通訊 (UM) 服務。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsHostedVoicemailPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsHostedVoicemailPolicy"}

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
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要移除之託管語音信箱原則的唯一識別碼。這個識別碼包括範圍 (以全域而言)、範圍和網站 (指網站原則，例如 site:Redmond) 或原則名稱 (指個別使用者原則，例如 HVUserPolicy)。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要刪除裝載語音信箱原則之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令來傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.HostedVoicemailPolicy 物件。接受管線傳送的主控語音信箱原則物件輸入。

## 傳回類型

此 Cmdlet 不會傳回物件，而會移除 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.HostedVoicemailPolicy 類型的物件。

## 請參閱

#### 其他資源

[New-CsHostedVoicemailPolicy](new-cshostedvoicemailpolicy.md)  
[Set-CsHostedVoicemailPolicy](set-cshostedvoicemailpolicy.md)  
[Get-CsHostedVoicemailPolicy](get-cshostedvoicemailpolicy.md)  
[Grant-CsHostedVoicemailPolicy](grant-cshostedvoicemailpolicy.md)

