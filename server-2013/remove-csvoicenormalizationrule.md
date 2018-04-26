---
title: Remove-CsVoiceNormalizationRule
TOCTitle: Remove-CsVoiceNormalizationRule
ms:assetid: 6a1bf26c-d95b-4a03-8d2d-c17159dcb9be
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398501(v=OCS.15)
ms:contentKeyID: 49291203
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsVoiceNormalizationRule

 

_**上次修改主題的時間：** 2015-03-09_

移除語音正規化規則。語音正規化規則可用於將電話撥號要求 (例如撥打外線之前先撥 9) 轉換成 Lync Server 所使用的 E.164 電話號碼格式。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsVoiceNormalizationRule -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會移除 Identity 為 site:Redmond/SeattleRule1 的語音正規化規則。

    Remove-CsVoiceNormalizationRule -Identity site:Redmond/SeattleRule1

## 範例 2

此範例會從 Redmond 網站中移除所有語音正規化規則。

    Remove-CsVoiceNormalizationRule -Identity site:Redmond

## 詳細描述

此 Cmdlet 會移除具名的語音正規化規則。這些規則是電話授權和電話路由的必要部分。它們定義將號碼從內部 Lync Server 格式轉換 (或轉譯) 為標準 (E.164) 格式的需求。了解規則運算式對於定義將要轉譯的號碼模式很有幫助。

使用此 Cmdlet 所移除的規則會從組織的撥號對應表中刪除，所以 **Get-CsVoiceNormalizationRule** Cmdlet 不會再傳回這些規則，而這些規則也不會出現在呼叫 **Get-CsDialPlan** Cmdlet 所傳回的 NormalizationRules 屬性中。也就是說，呼叫 **Remove-CsVoiceNormalizationRule** Cmdlet 可能會導致撥號對應表沒有正規化規則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsVoiceNormalizationRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsVoiceNormalizationRule"}

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
<td><p>要移除之規則的唯一識別身分。如果指定的 Identity 包含範圍，後面緊接著正斜線和名稱 (例如：site:Redmond/Rule1，其中 site:Redmond 為範圍，而 Rule1 為名稱)，擁有該唯一 Identity 的規則會遭到移除。如果傳遞給 Identity 的值僅包含範圍 (site:Redmond)，則會移除該範圍的所有正規化規則。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule 物件。接受管線傳送的語音正規化規則物件輸入。

## 傳回類型

此 Cmdlet 會刪除 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule 類型的物件。

## 請參閱

#### 其他資源

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[Remove-CsDialPlan](remove-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)

