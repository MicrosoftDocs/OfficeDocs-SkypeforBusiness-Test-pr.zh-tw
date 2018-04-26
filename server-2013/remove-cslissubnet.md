---
title: Remove-CsLisSubnet
TOCTitle: Remove-CsLisSubnet
ms:assetid: f8a87038-cc71-4fec-8496-574da0aa963f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413053(v=OCS.15)
ms:contentKeyID: 49292870
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsLisSubnet

 

_**上次修改主題的時間：** 2015-03-09_

移除位置資訊伺服器 (LIS) 子網路。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsLisSubnet -Subnet <String> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會針對 IP 位址為 192.10.10.0 的子網路移除 LIS 子網路位置項目。此範例中的命令只包含一個 (必要) 參數：Subnet。此範例中的 Subnet 值為 IPv4 位址，192.10.10.0。

如果這個子網路與某個位置相關聯，則無法移除該位置，將只會從位置對應中移除子網路。

    Remove-CsLisSubnet -Subnet 192.10.10.0

## 範例 2

此範例會移除與位置 Bldg30/Room1000 相關聯的所有子網路。範例首先呼叫 **Get-CsLisSubnet** Cmdlet，這會傳回所有 LIS 子網路的集合。此集合將傳送到 **Where-Object** Cmdlet，這會找到該集合中 Location 屬性等於 (-eq) 字串 Bldg30/Room1000 的項目。最後，將這個含該 Location 的子網路集合傳送到 **Remove-CsLisSubnet** Cmdlet，它會移除該集合中的每個項目。

請注意，如同範例 1，不會從位置資料庫中移除任何位置，只會移除參照這些位置的子網路。您可以呼叫 **Remove-CsLisLocation** Cmdlet 來移除這些位置。

    Get-CsLisSubnet | Where-Object {$_.Location -eq "Bldg30/Room1000"} | Remove-CsLisSubnet

## 詳細描述

增強型 9-1-1 (E9-1-1) 讓緊急電話接線生不必須詢問來電者的位置資訊，就能找出來電者的位置。當來電者是從 Voice over Internet Protocol (VoIP) 連線撥話時，必須根據各種連線係數來擷取該資訊。VoIP 系統管理員必須設定位置對應圖 (稱做接線圖) 來判定來電者的的位置。此 Cmdlet 會從位置組態資料庫移除子網路。移除子網路將不會移除與該子網路相關聯的位置。使用 **Remove-CsLisLocation** Cmdlet 可移除位置。

如果您嘗試移除不存在的子網路，則系統將不會採取任何動作，而您將不會收到任何錯誤或警告訊息。

誰可以執行這個 Cmdlet：根據預設，下列群組成員已獲得授權，可執行 **Remove-CsLisSubnet** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsLisSubnet"}

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
<td><p><em>Subnet</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>您要移除之子網路的 IP 位址。此值必須是 IPv4 位址 (以句點區隔位數，例如 192.0.2.0)。</p></td>
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

接受位置資訊伺服器 (LIS) 子網路物件的管線傳送資料。

## 傳回類型

此 Cmdlet 會移除 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Set-CsLisSubnet](set-cslissubnet.md)  
[Get-CsLisSubnet](get-cslissubnet.md)  
[Remove-CsLisLocation](remove-cslislocation.md)

