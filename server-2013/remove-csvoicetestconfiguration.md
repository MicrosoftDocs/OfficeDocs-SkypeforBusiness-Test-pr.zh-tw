---
title: Remove-CsVoiceTestConfiguration
TOCTitle: Remove-CsVoiceTestConfiguration
ms:assetid: abe27005-8325-47d7-8c7c-12bb831b87c7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412813(v=OCS.15)
ms:contentKeyID: 49291963
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsVoiceTestConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除用於測試電話號碼是否符合指定路由與規則的語音測試組態。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsVoiceTestConfiguration -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會移除 Identity 為 TestConfig1 的語音測試組態設定。

    Remove-CsVoiceTestConfiguration -Identity TestConfig1

## 範例 2

這個範例會移除 Identity 中包含字串 test 之任何設定的所有語音測試組態設定。命令會先呼叫 **Get-CsVoiceTestConfiguration** Cmdlet 搭配 Filter 參數，以擷取 Identity 值中包含字串 "test" 的所有語音測試設定。然後再將產生的設定集管線傳送至 **Remove-CsVoiceTestConfiguration** Cmdlet 加以移除。

    Get-CsVoiceTestConfiguration -Filter *test* | Remove-CsVoiceTestConfiguration

## 詳細描述

在實作語音路由和語音原則之前，最好先以不同的電話號碼來測試，以確保結果符合您的預期。完成這些測試且不再需要它們後，請使用這個 Cmdlet 將其移除。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsVoiceTestConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsVoiceTestConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>唯一識別您要移除之測試設定的字串。</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration 物件。接受管線傳送的語音測試組態物件輸入。

## 傳回類型

移除 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration 類型的物件。

## 請參閱

#### 其他資源

[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Set-CsVoiceTestConfiguration](set-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)  
[Test-CsVoiceTestConfiguration](test-csvoicetestconfiguration.md)

