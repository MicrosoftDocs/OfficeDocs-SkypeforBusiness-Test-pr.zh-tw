---
title: Get-CsLisPort
TOCTitle: Get-CsLisPort
ms:assetid: c755aa8c-e842-4bb8-bdbf-d61a364eb0bc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398820(v=OCS.15)
ms:contentKeyID: 49292270
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsLisPort

 

_**上次修改主題的時間：** 2015-03-09_

從位置組態資料庫擷取一或多個連接埠。每個連接埠都可關聯一個位置。在此情況下，此 Cmdlet 也會擷取連接埠的位置資訊。增強型 9-1-1 (E9-1-1) Enterprise Voice 實作會利用此位置關聯，通知緊急服務接線生來電者的位置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsLisPort

## 範例

## 範例 1

範例 1 會擷取所有位置資訊伺服器 (LIS) 連接埠和已在 Lync Server 部署中定義的所有相關位置。

    Get-CsLisPort

## 範例 2

此範例會擷取與 Redmond 城市中某個位置相關聯之所有連接埠的所有資訊。命令會先呼叫 **Get-CsLisPort** Cmdlet，以擷取所有連接埠位置關聯。然後將此連接埠位置集合管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會檢查集合中每一個項目的 City 屬性，以判斷值是否等於 (-eq) Redmond。

    Get-CsLisPort | Where-Object {$_.City -eq "Redmond"}

## 詳細描述

增強型 9-1-1 讓緊急電話接線生不必詢問來電者的位置資訊，就能找出來電者的位置。當來電者是從 Voice over Internet Protocol (VoIP) 連線撥話時，必須根據各種連線係數來擷取該資訊。VoIP 系統管理員必須設定位置對應圖 (稱做接線圖) 來判定來電者的的位置。此 Cmdlet 能根據實體位置和用戶端藉以進行連接之連接埠的關聯擷取資訊。

這個 Cmdlet 不接受任何參數 (除非是 Windows PowerShell 一般參數)。此 Cmdlet 會將所有的連接埠執行個體擷取為位置對應。若要縮小所擷取資訊的範圍，必須將此 Cmdlet 的輸出管線傳送到另一個 Windows PowerShell Cmdlet，例如 **Where-Object** Cmdlet 或 **Select-Object** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsLisPort** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsLisPort"}

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

此 Cmdlet 會擷取 System.Management.Automation.PSCustomObject 類型的一或多個物件。

## 請參閱

#### 其他資源

[Remove-CsLisPort](remove-cslisport.md)  
[Set-CsLisPort](set-cslisport.md)

