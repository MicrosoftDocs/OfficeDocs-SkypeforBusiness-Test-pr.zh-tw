---
title: Remove-CsLisSwitch
TOCTitle: Remove-CsLisSwitch
ms:assetid: 53456988-4b37-4f34-825d-bebee5124856
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398352(v=OCS.15)
ms:contentKeyID: 49290926
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsLisSwitch

 

_**上次修改主題的時間：** 2015-03-09_

移除位置資訊伺服器 (LIS) 網路交換器。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsLisSwitch -ChassisID <String> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會移除 MAC 位址 (ChassisID) 為 99-99-99-99-99-99 的 LIS 交換器。

如果有連接埠參照 ChassisID，此命令便不會成功。同時，如果此交換器與位置產生關聯，則系統不會移除該位置，只會將交換器自位置對應中移除。

    Remove-CsLisSwitch -ChassisID 99-99-99-99-99-99

## 範例 2

此範例會移除所有沒有城市的交換器。範例一開始會呼叫 **Get-CsLisSwitch** Cmdlet，這會傳回所有交換器的集合。此集合會傳送到 **Where-Object** Cmdlet，此 Cmdlet 會尋找該集合中 City 屬性為空白的項目，換句話說是 City 等於 (-eq) 空白字串 (“”) 的項目。最後，我們會將這個沒有城市的交換器集合傳送到 **Remove-CsLisSwitch** Cmdlet，以移除該集合中的所有項目。

請注意，如同範例 1 所示，沒有位置會從位置資料庫中移除，只會移除參照那些位置的交換器。在此狀況下，這表示位置資料庫中的無效位置 (這些位置無效的原因為 City 是位置的必要屬性) 也應刪除。您可以呼叫 **Remove-CsLisLocation** Cmdlet 來移除這些位置。

    Get-CsLisSwitch | Where-Object {$_.City -eq ""} | Remove-CsLisSwitch

## 詳細描述

增強型 9-1-1 (E9-1-1) 讓緊急電話接線生不必須詢問來電者的位置資訊，就能找出來電者的位置。當來電者是從 Voice over Internet Protocol (VoIP) 連線撥話時，必須根據各種連線係數來擷取該資訊。VoIP 系統管理員必須設定位置對應圖 (稱做接線圖) 來判定來電者的的位置。此 Cmdlet 會將交換器自位置組態資料庫中移除。移除交換器並不會移除實際的位置，只會移除交換器。若要移除位置，請呼叫 **Remove-CsLisLocation** Cmdlet。

如果連接埠有使用交換器的 ChassisID，您便無法移除交換器(請執行以下命令找出連接埠使用哪些 ChassisID：Get-CsLisPort | Select-Object ChassisID)。您必須先移除所有使用指定之 ChassisID 的連接埠，才能移除交換器。

如果您嘗試移除的交換器並不存在，系統不會採取任何的動作，您也不會收到錯誤或警告訊息。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsLisSwitch** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsLisSwitch"}

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
<td><p><em>ChassisID</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>網路交換器的媒體存取控制 (MAC) 位址。此值的格式為 nn-nn-nn-nn-nn-nn，例如 12-34-56-78-90-ab。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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

接受 LIS 交換器物件管線傳送的輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Set-CsLisSwitch](set-cslisswitch.md)  
[Get-CsLisSwitch](get-cslisswitch.md)  
[Remove-CsLisLocation](remove-cslislocation.md)  
[Get-CsLisPort](get-cslisport.md)

