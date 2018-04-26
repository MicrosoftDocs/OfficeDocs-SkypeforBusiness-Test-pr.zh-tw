---
title: Remove-CsDialPlan
TOCTitle: Remove-CsDialPlan
ms:assetid: 99845b82-1730-494a-8f47-2dec5ef177c1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398791(v=OCS.15)
ms:contentKeyID: 49291776
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDialPlan

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的撥號對應表。此 Cmdlet 也可用於移除全域撥號對應表。移除全域撥號對應表並不會真正移除撥號對應表，而只會將設定重設為預設值。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsDialPlan -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 使用 **Remove-CsDialPlan** Cmdlet 來刪除 Identity 為 RedmondDialPlan 的個別使用者撥號對應表。請注意，刪除撥號對應表時，對於原先獲指派現已刪除之撥號對應表的使用者，不一定要指派新的對應表。這些使用者將會改用指派給服務或網站的撥號對應表，或全域對應表。

    Remove-CsDialPlan -Identity RedmondDialPlan

## 範例 2

範例 2 會刪除描述中包含 Redmond 一字的所有撥號對應表。為達成此目的，命令會先呼叫 **Get-CsDialPlan** Cmdlet，以傳回所有設定供組織使用之撥號對應表的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet 套用篩選，以將傳回的資料限制為描述中包含 Redmond 一字的設定檔。接著將篩選後的集合傳遞給 **Remove-CsDialPlan** Cmdlet，以移除集合中所有的撥號對應表。

    Get-CsDialPlan | Where-Object {$_.Description -match "Redmond"} | Remove-CsDialPlan

## 詳細描述

此 Cmdlet 會移除現有的撥號對應表 (又稱為位置設定檔)。撥號對應表可提供 Enterprise Voice 使用者撥打電話所需的資訊。會議服務員應用程式也會在執行電話撥入式會議時使用撥號對應表。撥號對應表可指定所要套用的正規化規則，以及撥打外線時是否需要先撥首碼。

注意：移除撥號對應表也會移除任何相關聯的正規化規則。如果移除全域撥號對應表，也會移除任何相關聯的正規化規則，但是會建立預設的全域正規化規則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsDialPlan** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDialPlan"}

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
<td><p>您要移除之撥號對應表的唯一識別碼。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile 物件。**Remove-CsDialPlan** Cmdlet 接受管線傳送的撥號對應表物件輸入。

## 傳回類型

此 Cmdlet 會移除 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsDialPlan](new-csdialplan.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Grant-CsDialPlan](grant-csdialplan.md)  
[Test-CsDialPlan](test-csdialplan.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)

