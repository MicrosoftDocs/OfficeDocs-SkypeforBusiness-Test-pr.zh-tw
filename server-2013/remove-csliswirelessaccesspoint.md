---
title: Remove-CsLisWirelessAccessPoint
TOCTitle: Remove-CsLisWirelessAccessPoint
ms:assetid: 656190b0-bde0-4a92-a6b5-b96a389c4863
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398461(v=OCS.15)
ms:contentKeyID: 49291145
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsLisWirelessAccessPoint

 

_**上次修改主題的時間：** 2015-03-09_

移除位置資訊伺服器 (LIS) 的無線存取點 (WAP)。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsLisWirelessAccessPoint -BSSID <String> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會移除 BSSID 為 99-99-99-99-99-99 的 LIS WAP 位置。

如果此 WAP 與位置之間有關聯，系統不會移除該位置，只會將 WAP 自位置對應中移除。

    Remove-CsLisWirelessAccessPoint -BSSID 99-99-99-99-99-99

## 範例 2

此範例會移除 Building 30 中所有的 WAP。範例一開始會先呼叫 **Get-CsLisWirelessAccessPoint** Cmdlet，這會傳回所有 WAP 的集合。此集合會傳送到 **Where-Object** Cmdlet，這會在該集合中尋找 Location 屬性值任何一處有包含字串 Bldg30 的項目，換句話說就是 Location 類似 (-like) Bldg30 的項目。最後我們將 Building 30 中的這個 WAP 集合傳送到 **Remove-CsLisWirelessAccessPoint** Cmdlet，這會移除該集合中的所有一切。

請注意，如同範例 1 所示，沒有位置會從位置組態資料庫中移除，只會移除參照那些位置的 WAP。

    Get-CsLisWirelessAccessPoint | Where-Object {$_.Location -like "*Bldg30*"} | Remove-CsLisWirelessAccessPoint

## 詳細描述

增強型 9-1-1 讓緊急電話接線生不必詢問來電者的位置資訊，就能找出來電者的位置。當來電者是從 Voice over Internet Protocol (VoIP) 連線撥話時，必須根據各種連線係數來擷取該資訊。VoIP 系統管理員必須設定位置對應圖 (稱做接線圖) 來判定來電者的的位置。此 Cmdlet 會將 WAP 自位置組態資料庫中移除。移除 WAP 並不會移除與該 WAP 關聯的位址。使用 **Remove-CsLisLocation** Cmdlet 可移除位置。

如果您嘗試移除的 WAP 並不存在，系統不會採取任何的動作，您也不會收到錯誤或警告訊息。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsLisWirelessAccessPoint** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsLisWirelessAccessPoint"}

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
<td><p><em>BSSID</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要移除的無線存取點基本服務集識別碼 (BSSID)。此值的格式為 nn-nn-nn-nn-nn-nn，例如 12-34-56-78-90-ab。</p></td>
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

接受管線傳送的 LIS 無線存取點物件輸入。

## 傳回類型

此 Cmdlet 會移除 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Set-CsLisWirelessAccessPoint](set-csliswirelessaccesspoint.md)  
[Get-CsLisWirelessAccessPoint](get-csliswirelessaccesspoint.md)  
[Remove-CsLisLocation](remove-cslislocation.md)

