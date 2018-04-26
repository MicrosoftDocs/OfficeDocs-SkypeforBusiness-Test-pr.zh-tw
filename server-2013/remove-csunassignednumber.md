---
title: Remove-CsUnassignedNumber
TOCTitle: Remove-CsUnassignedNumber
ms:assetid: 13095593-92d3-4790-99a5-5df4610652cb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398209(v=OCS.15)
ms:contentKeyID: 49290157
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsUnassignedNumber

 

_**上次修改主題的時間：** 2015-03-09_

移除現有未指派號碼的範圍，以及套用到這些號碼的路由規則。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsUnassignedNumber -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會移除 Identity 為 UNSet1 的未指派號碼設定。

    Remove-CsUnassignedNumber -Identity UNSet1

## 範例 2

範例 2 會移除已指派宣告名稱包含 Welcome 字串的所有未指派號碼。命令一開始會呼叫 **Get-CsUnassignedNumber** Cmdlet，以傳回所有未指派號碼設定集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以將集合限縮在 AnnouncementName 包含 (-match) Welcome 字串的未指派號碼設定。最後，將所得到的集合傳遞到 **Remove-CsUnassignedNumber** Cmdlet，以移除集合中的所有內容。

    Get-CsUnassignedNumber | Where-Object {$_.AnnouncementName -match "Welcome"} | Remove-CsUnassignedNumber

## 詳細描述

未指派號碼是指已指派給組織，但尚未指派給特定使用者或電話的電話號碼。您可設定 Lync Server 在有人撥打未指派號碼時，會將撥打的電話路由到適當目的地。此 Cmdlet 會移除定義該路由的設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsUnassignedNumber** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsUnassignedNumber"}

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
<td><p>要移除之未指派號碼範圍的唯一名稱。</p></td>
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

Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange 物件。接受未指派號碼物件管線傳送的輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange 類型的物件。

## 請參閱

#### 其他資源

[New-CsUnassignedNumber](new-csunassignednumber.md)  
[Set-CsUnassignedNumber](set-csunassignednumber.md)  
[Get-CsUnassignedNumber](get-csunassignednumber.md)  
[Get-CsAnnouncement](get-csannouncement.md)  
[Get-CsExUmContact](get-csexumcontact.md)

