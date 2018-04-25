---
title: Get-CsLisSubnet
TOCTitle: Get-CsLisSubnet
ms:assetid: 670b50b9-a5ab-4b70-bdb9-bdf3c1b09d0b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398473(v=OCS.15)
ms:contentKeyID: 49291162
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsLisSubnet

 

_**上次修改主題的時間：** 2015-03-09_

從位置組態資料庫擷取一或多個子網路。每個子網路都可關聯一個位置。在此情況下，此 Cmdlet 也會擷取子網路的位置資訊。增強型 9-1-1 (E9-1-1) Enterprise Voice 實作會利用此位置關聯，通知緊急服務接線生來電者的位置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsLisSubnet

## 範例

## 範例 1

範例 1 會擷取已在 Lync Server 部署中定義的所有位置資訊伺服器 (LIS) 子網路。

    Get-CsLisSubnet

## 範例 2

此範例會擷取 IP 位址為 192.0.10.0 之子網路的所有資訊。命令會先呼叫 **Get-CsLisSubnet** Cmdlet 擷取所有子網路位置關聯。接著會將此子網路位置的集合管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會檢查集合中每個項目的 Subnet 屬性，以判定其值是否等於 (-eq) 192.0.10.0。因為 Subnet ID 必須是唯一的，所以此命令最多只會傳回一個物件。

    Get-CsLisSubnet | Where-Object {$_.Subnet -eq "192.0.10.0"}

## 詳細描述

增強型 9-1-1 讓緊急電話接線生不必詢問來電者的位置資訊，就能找出來電者的位置。當來電者是從 Voice over Internet Protocol (VoIP) 連線撥話時，必須根據各種連線係數來擷取該資訊。VoIP 系統管理員必須設定位置對應圖 (稱做接線圖) 來判定來電者的的位置。此 Cmdlet 會擷取實體位置與用於路由來電之子網路間的關聯資訊。

這個 Cmdlet 不接受任何參數 (除非是 Windows PowerShell 一般參數)。Cmdlet 會擷取子網路對位置對應的所有執行個體。若要縮小所擷取資訊的範圍，必須將此 Cmdlet 的輸出管線傳送到另一個 Windows PowerShell Cmdlet，例如 **Where-Object** Cmdlet 或 **Select-Object** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsLisSubnet** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsLisSubnet"}

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
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>此 Cmdlet 只提供一般的 Windows PowerShell 參數。</p></td>
<td><p></p></td>
<td><p></p></td>
<td> </td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

此 Cmdlet 會擷取 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsLisSubnet](remove-cslissubnet.md)  
[Set-CsLisSubnet](set-cslissubnet.md)

