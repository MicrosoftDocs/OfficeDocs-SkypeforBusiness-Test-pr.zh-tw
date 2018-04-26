---
title: Remove-CsVoicePolicy
TOCTitle: Remove-CsVoicePolicy
ms:assetid: 4d3e67be-c094-415f-b1e6-0719dec6f3fc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398309(v=OCS.15)
ms:contentKeyID: 49290864
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsVoicePolicy

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的語音原則。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsVoicePolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會移除 UserVoicePolicy1 個別使用者語音原則設定。

    Remove-CsVoicePolicy -Identity UserVoicePolicy1

## 範例 2

此範例會移除所有可指派給特定使用者的語音原則設定。首先呼叫 **Get-CsVoicePolicy** Cmdlet 並搭配 tag\* 的 Filter，擷取所有個別使用者語音原則。接著，將該原則集合傳送給 **Remove-CsVoicePolicy** Cmdlet 以移除。

    Get-CsVoicePolicy -Filter tag* | Remove-CsVoicePolicy

## 詳細描述

此 Cmdlet 會移除現有的語音原則。語音原則可用來管理 Enterprise Voice 相關功能，例如同時響鈴 (每次有人撥打到您的辦公室電話時，能夠讓第二支電話響起) 和來電轉接。此 Cmdlet 也可用來移除全域語音原則。但在此情況下，不會真的移除原則；而只是將原則設定重設為預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsVoicePolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsVoicePolicy"}

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
<td><p>指定要移除之原則的範圍和 (在某些情況下) 名稱的唯一識別碼。</p></td>
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
<td><p>要刪除語音原則之 Office 365 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令來傳回每位租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>倘若使用的是 Windows PowerShell 遠端工作階段並僅連線至 商務用 Skype Online，則無需包含 Tenant 參數。相反地，系統將會根據您的連線資訊自動填入租用戶識別碼。Tenant 參數主要用於混合式部署。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy 物件。接受管線傳送的語音原則物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)

