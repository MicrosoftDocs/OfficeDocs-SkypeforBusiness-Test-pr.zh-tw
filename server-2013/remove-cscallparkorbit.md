---
title: Remove-CsCallParkOrbit
TOCTitle: Remove-CsCallParkOrbit
ms:assetid: b8e7c236-f8de-45bd-966b-60c815b37aed
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412901(v=OCS.15)
ms:contentKeyID: 49292122
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCallParkOrbit

 

_**上次修改主題的時間：** 2015-03-09_

移除特定的通話駐留軌道範圍。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsCallParkOrbit -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會使用 **Remove-CsCallParkOrbit** Cmdlet，來刪除名為 Redmond CPO 1 的通話駐留軌道範圍。

    Remove-CsCallParkOrbit -Identity "Redmond CPO 1"

## 範例 2

此範例中的命令會移除針對組織定義的所有通話駐留範圍。命令會先不使用任何參數而直接呼叫 **Get-CsCallParkOrbit** Cmdlet，以擷取所有已定義的通話駐留範圍。然後再將通話駐留範圍集合傳送到 **Remove-CsCallParkOrbit** Cmdlet，以移除每個通話駐留範圍。

    Get-CsCallParkOrbit | Remove-CsCallParkOrbit

## 範例 3

此命令會移除 Identity 包含字串 "Redmond" 的所有通話駐留軌道範圍，如 "Redmond 501"、"CP Redmond 1" 及 "ARedmond"。命令會先呼叫 **Get-CsCallParkOrbit** Cmdlet 搭配 Filter 參數，以擷取 Identity 包含字串 Redmond 的所有通話駐留軌道範圍。然後，此集合會管線傳送到 **Remove-CsCallParkOrbit** Cmdlet，以移除集合中的所有內容。

    Get-CsCallParkOrbit -Filter *Redmond* | Remove-CsCallParkOrbit

## 詳細描述

**Remove-CsCallParkOrbit** Cmdlet 會刪除含有已傳送給 Identity 參數 (此為必要參數) 之名稱的通話保留範圍。組織中每個通話保留範圍都必須具有唯一的號碼範圍。移除通話保留範圍會釋出該通話保留範圍中的範圍。接著釋出的號碼可用在新定義的通話保留範圍中。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsCallParkOrbit** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCallParkOrbit"}

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
<td><p>通話駐留範圍的名稱。此名稱由系統管理員在定義通話保留範圍時指派。</p></td>
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

Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit 物件。接受管線傳送的通話保留範圍物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit 類型的物件。

## 請參閱

#### 其他資源

[New-CsCallParkOrbit](new-cscallparkorbit.md)  
[Set-CsCallParkOrbit](set-cscallparkorbit.md)  
[Get-CsCallParkOrbit](get-cscallparkorbit.md)

