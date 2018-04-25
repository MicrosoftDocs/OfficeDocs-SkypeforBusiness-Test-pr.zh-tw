---
title: Get-CsLisCivicAddress
TOCTitle: Get-CsLisCivicAddress
ms:assetid: 6538b811-6b74-4c57-95f7-e1496df62e7f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398459(v=OCS.15)
ms:contentKeyID: 49291134
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsLisCivicAddress

 

_**上次修改主題的時間：** 2015-03-09_

僅擷取增強型 9-1-1 (E9-1-1) 之位置組態資料庫中一或多個位置的位址部分。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsLisCivicAddress

## 範例

## 範例 1

此範例會從位置資料庫擷取所有的市街地址。**Get-CsLisCivicAddress** Cmdlet 不接受任何參數 (除非是一般 Windows PowerShell 參數，例如 Verbose)。因此對 **Get-CsLisCivicAddress** Cmdlet 的任何呼叫將一律傳回所有的市街地址。如需允許您擷取更特定結果的命令，請參閱範例 2。

    Get-CsLisCivicAddress

## 範例 2

此範例會擷取 Redmond 城市中所有的市街地址。範例一開始會呼叫 **Get-CsLisCivicAddress** Cmdlet，這會擷取位置資料庫中所有市街地址的集合。接著將此集合管線傳送到 **Where-Object** Cmdlet，這會只傳回集合中 City 屬性值等於 (-eq) Redmond 的項目。

    Get-CsLisCivicAddress | Where-Object {$_.City -eq "Redmond"}

## 範例 3

範例 3 會擷取已對照主要街道地址指南 (MSAG) 驗證的所有位置資訊伺服器 (LIS) 市街地址。

    Get-CsLisCivicAddress | Where-Object {$_.MSAGValid -eq $true}

## 詳細描述

E9-1-1 可讓接聽緊急電話的人能夠判定來電者的地理位置，而無須向來電者詢問該資訊。Lync Server 中，是根據來電者連接埠、子網路、交換器或無線存取點與特定位置間的對應，來判定來電者的位置。此 Cmdlet 會擷取與這些位置關聯的一或多個地址。

此 Cmdlet 與 **Get-CsLisLocation** Cmdlet 的不同之處是，它只會傳回唯一的地址。它不會傳回公司名稱或位置名稱；只會傳回地址資訊。它也會傳回旗標 (MSAGValid)，此旗標會指示是否已對照主要街道地址指南來驗證地址。執行 **Test-CsLisCivicAddress** Cmdlet 可自動更新此旗標。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsLisCivicAddress** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsLisCivicAddress"}

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

[Test-CsLisCivicAddress](test-csliscivicaddress.md)  
[Get-CsLisLocation](get-cslislocation.md)

