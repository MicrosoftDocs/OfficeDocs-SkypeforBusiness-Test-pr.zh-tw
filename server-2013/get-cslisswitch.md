---
title: Get-CsLisSwitch
TOCTitle: Get-CsLisSwitch
ms:assetid: 2b09e8f1-4930-4ac2-8f6f-48c08cd890c5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425769(v=OCS.15)
ms:contentKeyID: 49290432
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsLisSwitch

 

_**上次修改主題的時間：** 2015-03-09_

從位置組態資料庫擷取一或多個網路交換器。每個交換器都可關聯一個位置，而即便如此，此 Cmdlet 仍會擷取交換器的位置資訊。增強型 9-1-1 (E9-1-1) Enterprise Voice 實作會利用此位置關聯，通知緊急服務接線生來電者的位置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsLisSwitch

## 範例

## 範例 1

範例 1 擷取 Lync Server 部署中已定義的所有位置資訊伺服器 (LIS) 交換器。

    Get-CsLisSwitch

## 範例 2

此範例會擷取 ChassisID 等於 99-99-99-99-99-99 之所有交換器的所有資訊。由於 ChassisID 必須是唯一的，因此這個命令最多只會擷取一個交換器位置。此命令會從呼叫 **Get-CsLisSwitch** Cmdlet 開始，以擷取所有交換器位置關聯。這個交換器位置的集合會管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會檢查集合中每一個項目的 ChassisID 屬性，並傳回 ChassisID 值為 99-99-99-99-99-99 的項目。

    Get-CsLisSwitch | Where-Object {$_.ChassisID -eq "99-99-99-99-99-99"}

## 範例 3

此範例會擷取與 Redmond 市中某位置相關聯之所有交換器的所有資訊。此命令會從呼叫 **Get-CsLisSwitch** Cmdlet 開始，以擷取所有交換器位置關聯。這個交換器位置的集合會管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會檢查集合中每一個項目的 City 屬性，以判斷值是否等於 (-eq) Redmond。

    Get-CsLisSwitch | Where-Object {$_.City -eq "Redmond"}

## 詳細描述

增強型 9-1-1 讓緊急電話接線生不必詢問來電者的位置資訊，就能找出來電者的位置。當來電者是從 Voice over Internet Protocol (VoIP) 連線撥話時，必須根據各種連線係數來擷取該資訊。VoIP 系統管理員必須設定可判斷來電者位置的位置圖 (稱為線路圖)。此 Cmdlet 會擷取實體位置和用戶端用於連接之網路交換器之間的關聯性資訊。

這個 Cmdlet 不接受任何參數 (除非是 Windows PowerShell 一般參數)。此 Cmdlet 會擷取交換器之位置對應的所有執行個體。若要縮小所擷取資訊的範圍，您必須將這個 Cmdlet 的輸出傳送到另一個 Windows PowerShell Cmdlet，例如 **Where-Object** Cmdlet 或 **Select-Object** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsLisSwitch** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsLisSwitch"}

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

此 Cmdlet 會擷取一或多個 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsLisSwitch](remove-cslisswitch.md)  
[Set-CsLisSwitch](set-cslisswitch.md)

