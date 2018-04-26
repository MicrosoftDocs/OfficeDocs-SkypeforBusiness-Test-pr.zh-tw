---
title: Get-CsLisLocation
TOCTitle: Get-CsLisLocation
ms:assetid: aede2266-5af4-4973-9db1-a7b505c62057
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412834(v=OCS.15)
ms:contentKeyID: 49292015
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsLisLocation

 

_**上次修改主題的時間：** 2015-03-09_

從增強型 9-1-1 (E9-1-1) 位置組態資料庫中擷取一或多個位置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsLisLocation [-Unreferenced <SwitchParameter>]

## 範例

## 範例 1

呼叫不含任何參數的 **Get-CsLisLocation** Cmdlet 會擷取位置組態資料庫中定義的所有位置。

    Get-CsLisLocation

## 範例 2

Unreferenced 參數不接受值。它只是一個參數，告訴 **Get-CsLisLocation** Cmdlet 只要傳回與連接埠、交換器、子網路，或無線存取點無關聯的位置。

    Get-CsLisLocation -Unreferenced

## 範例 3

若要擷取特定的 LIS 位置，必須呼叫 **Get-CsLisLocation** Cmdlet 以擷取所有位置，然後將該位置集合管線傳送到 **Where-Object** Cmdlet，以將集合的範圍縮小到您要尋找的特定位置。範例 3 便是這麼做：它會使用 **Get-CsLisLocation** Cmdlet 和 **Where-Object** Cmdlet，來擷取所有 Location 屬性等於字串 NorthCampus 的位置 (請注意，我們使用 –ceq 比較運算子。此運算子會進行區分大小寫的比較。意思是說，在這個範例中，只會傳回 Location 值為 NorthCampus 的位置；northcampus、Northcampus 等都不會傳回)。

    Get-CsLisLocation | Where-Object {$_.Location -ceq "NorthCampus"}

## 詳細描述

E9-1-1 可讓接聽緊急電話的人能夠判定來電者的地理位置，而無需向來電者詢問該資訊。Lync Server 是根據來電者連接埠、子網路、交換器或無線存取點與特定位置間的對應，來判定來電者的位置。此 Cmdlet 會擷取其中一或多個位置。

此 Cmdlet 與 **Get-CsLisCivicAddress** Cmdlet 的差異在於，除了擷取地址資訊外，**Get-CsLisLocation** Cmdlet 也會擷取位置名稱以及與此位置相關聯的公司名稱。**Get-CsLisCivicAddress** Cmdlet 只會擷取地址資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsLisLocation** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsLisLocation"}

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
<td><p><em>Unreferenced</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>加上此參數就只會擷取與連接埠、子網路、交換器或無線存取點無關的位置。換句話說，加上此參數擷取的所有位置，都是利用呼叫 <strong>Set-CsLisLocation</strong> Cmdlet 而建立的位置，或是指派到已不存在之位置資訊伺服器 (LIS) 連接埠、子網路或無線存取點的位置。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

此 Cmdlet 會傳回一或多個 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsLisLocation](remove-cslislocation.md)  
[Set-CsLisLocation](set-cslislocation.md)  
[Get-CsLisCivicAddress](get-csliscivicaddress.md)

