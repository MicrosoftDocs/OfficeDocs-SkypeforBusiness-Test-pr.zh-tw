---
title: Remove-CsVoiceConfiguration
TOCTitle: Remove-CsVoiceConfiguration
ms:assetid: 9b173dde-fa8e-4966-aa58-deff34625560
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398804(v=OCS.15)
ms:contentKeyID: 49291782
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsVoiceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

將語音設定重設為預設值。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsVoiceConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例將 Global (且只有) 語音設定重設為預設值。此動作會刪除所有已定義的語音測試設定，所以我們增加 Confirm 參數來接收提示，詢問在移除之前是否真的想要執行此動作。

    Remove-CsVoiceConfiguration -Identity Global -Confirm

## 詳細描述

語音測試設定可根據特定語音原則、路由和撥號對應表，用來測試電話號碼。此 Cmdlet 會移除全域 (且只有) 語音設定，這是針對 Lync Server 部署所定義的所有語音測試設定的容器。「移除」語音設定不會真的移除該設定，全域執行個體仍然存在。不過，它會將語音測試設定的清單設為預設值，也就是空的。

警告：移除語音設定 (將語音測試設定的清單設為空的) 會刪除所有針對 Lync Server 部署所定義的語音測試設定。呼叫此 Cmdlet 之後，呼叫 **Get-CsVoiceTestConfiguration** Cmdlet 不會傳回結果。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsVoiceConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsVoiceConfiguration"}

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
<td><p>要移除之語音設定的範圍。這個值必須是 Global。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration 物件。接受管線傳送的語音組態物件輸入。

## 傳回類型

此 Cmdlet 會移除 (重設) Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguratione 類型的物件。

## 請參閱

#### 其他資源

[Set-CsVoiceConfiguration](set-csvoiceconfiguration.md)  
[Get-CsVoiceConfiguration](get-csvoiceconfiguration.md)  
[Remove-CsVoiceTestConfiguration](remove-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)

