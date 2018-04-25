---
title: Remove-CsLisPort
TOCTitle: Remove-CsLisPort
ms:assetid: b8a648af-1064-4a1e-8462-f267b7b72be1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412899(v=OCS.15)
ms:contentKeyID: 49292119
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsLisPort

 

_**上次修改主題的時間：** 2015-03-09_

移除位置資訊伺服器 (LIS) 連接埠與位置的關聯。增強型 9-1-1 (E9-1-1) Enterprise Voice 實作會利用連接埠與位置之間的關聯，通知緊急服務接線生來電者的位置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsLisPort -ChassisID <String> -PortID <String> -PortIDSubType <InterfaceAlias | InterfaceName | LocallyAssigned> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會移除 MAC 位址 (ChassisID) 為 99-99-99-99-99-99、PortID 為 4200 且 PortIDSubType 為 1 的 LIS 連接埠 (請注意，值為 1 的 PortIDSubType 會轉換為 InterfaceAlias 的值。此參數和值也可以輸入如下：-PortIDSubType InterfaceAlias)

如果此連接埠與某個位置關聯，該位置不會被移除，只會從位置對應中移除此連接埠。

    Remove-CsLisPort -ChassisID 99-99-99-99-99-99 -PortID 4200 -PortIDSubType 1

## 範例 2

此範例會移除所有無門牌號碼的連接埠位置。範例首先呼叫 **Get-CsLisPort** Cmdlet，這會傳回所有 LIS 連接埠位置的集合。接著將此集合傳送給 **Where-Object** Cmdlet，由其尋找集合中 HouseNumber 屬性空白 (就是 HouseNumber 等於 (-eq) 空字串 (“”) 的項目。最後，我們將這個無門牌號碼的連接埠位置集合傳送給 **Remove-CsLisPort** Cmdlet，以移除此集合中的每個項目。

請注意，如範例 1 所示，不會從位置組態資料庫中移除任何位置，只有參考這些位置的連接埠會被移除。在此狀況下，這表示在位置資料庫中會出現應該要移除的無效位置 (它們無效是因為 HouseNumber 是位置的必要屬性)。您可以呼叫 **Remove-CsLisLocation** Cmdlet 來移除這些位置。

    Get-CsLisPort | Where-Object {$_.HouseNumber -eq ""} | Remove-CsLisPort

## 詳細描述

增強型 9-1-1 讓緊急電話接線生不必詢問來電者的位置資訊，就能找出來電者的位置。當來電者是從 Voice over Internet Protocol (VoIP) 連線撥話時，必須根據各種連線係數來擷取該資訊。VoIP 系統管理員必須設定位置對應圖 (稱做接線圖) 來判定來電者的的位置。此 Cmdlet 會從位置組態資料庫移除連接埠，藉以移除實際位置和連接埠之間的關聯，而通話是透過此關聯傳送。

移除連接埠位置並不會移除連接埠的實際位置，它只是移除連接埠。若要移除位置，請呼叫 **Remove-CsLisLocation** Cmdlet。移除連接埠不會同時移除含有指定 ChassisID 的交換器；若要移除交換器，請呼叫 **Remove-CsLisSwitch** Cmdlet。

如果您要移除的連接埠不存在，就不會有任何動作，您也不會收到錯誤或警告訊息。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsLisPort** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsLisPort"}

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
<td><p>連接埠交換器的媒體存取控制 (MAC) 位址。此值的格式為 nn-nn-nn-nn-nn-nn，例如 12-34-56-78-90-ab。</p></td>
</tr>
<tr class="even">
<td><p><em>PortID</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>您要移除的連接埠的 ID。</p></td>
</tr>
<tr class="odd">
<td><p><em>PortIDSubType</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Lis.PortIDSubType</p></td>
<td><p>您要移除的連接埠的子類型。此值可以輸入數值或字串，但必須是有效的子類型。有效的子類型為：</p>
<p>1: InterfaceAlias</p>
<p>5: InterfaceName</p>
<p>7: LocallyAssigned</p></td>
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

接受管線傳送的 LIS 連接埠物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Set-CsLisPort](set-cslisport.md)  
[Get-CsLisPort](get-cslisport.md)  
[Remove-CsLisLocation](remove-cslislocation.md)  
[Remove-CsLisSwitch](remove-cslisswitch.md)

