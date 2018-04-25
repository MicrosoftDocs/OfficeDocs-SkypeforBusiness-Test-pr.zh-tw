---
title: Test-CsLisCivicAddress
TOCTitle: Test-CsLisCivicAddress
ms:assetid: 4079e767-3339-40c9-b7cd-08ec6c9d2c25
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425914(v=OCS.15)
ms:contentKeyID: 49290708
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsLisCivicAddress

 

_**上次修改主題的時間：** 2015-03-09_

根據主要街道地址指南測試一或多個城市地址。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsLisCivicAddress [-City <String>] [-Confirm [<SwitchParameter>]] [-Country <String>] [-HouseNumber <String>] [-HouseNumberSuffix <String>] [-PostalCode <String>] [-PostDirectional <String>] [-PreDirectional <String>] [-State <String>] [-StreetName <String>] [-StreetSuffix <String>] [-UpdateValidationStatus <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此命令會對照主要街道地址指南，使用符合在這些參數中所指定值的屬性來驗證地址。請注意，在結尾處包含 UpdateValidationStatus 屬性：這會更新地址的 MSAGValid 屬性。

    Test-CsLisCivicAddress -HouseNumber 1234 -HouseNumberSuffix "" -PreDirectional "" -StreetName Main -StreetSuffix St -PostDirectional "" -City Redmond -State WA -PostalCode 99999 -Country US -UpdateValidationStatus

## 範例 2

此範例會顯示如何測試所有的 LIS 市街地址。範例首先會呼叫 **Get-CsLisCivicAddress** Cmdlet 以擷取在位置資料庫中定義的所有市街地址。這些地址便會傳送到 **Test-CsLisCivicAddress** Cmdlet，此 Cmdlet 會使用 E9-1-1 網路路由供應商 Web 服務以驗證每個地址。

    Get-CsLisCivicAddress | Test-CsLisCivicAddress -UpdateValidationStatus

## 詳細描述

在以增強型 9-1-1 (E9-1-1) 實作的 Enterprise Voice 中，系統會根據位置地圖來判定使用者的位置；位置地圖會將子網路、連接埠、交換器或無線存取點對應到位置(如果缺少與對應位置之間的連線，系統會要求使用者手動輸入位置)。E9-1-1 網路路由供應商必須對照主要街道地址指南(MSAG) 來驗證這些位置的地址。此 Cmdlet 使用供應商的 Web 服務來驗證對應的地址。您可以呼叫 **Set-CsLisServiceProvider** Cmdlet 來設定服務供應商。

如果您要更新市街地址的 MSAGValid 屬性，請確定在呼叫 **Test-CsLisCivicAddress** Cmdlet 時，將 UpdateValidationStatus 參數包含在內。使用**Get-CsLisCivicAddress** Cmdlet 以擷取市街地址。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsLisCivicAddress** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsLisCivicAddress"}

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
<td><p><em>City</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>城市位置。</p>
<p>最大長度：64 個字元。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Country</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此位置所在國家/地區。</p>
<p>最大長度：2 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>HouseNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>位置的門牌號碼。如為公司，則是公司所在地點的街道號碼。</p>
<p>最大長度：10 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>HouseNumberSuffix</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>門牌號碼的額外資訊，例如 1/2 或 A，舉例來說 1234 1/2 Oak Street 或 1234 A Elm Street。</p>
<p>最大長度：5 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>PostalCode</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>與此位置關聯的郵遞區號。</p>
<p>最大長度：10 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>PostDirectional</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>街道名稱的方向指定。例如 NE 或 NW 代表 Main Street NE 或 7th Avenue NW。</p>
<p>最大長度：2 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>PreDirectional</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>街道名稱的方向指定放在街道名稱前。例如 NE 或 NW 代表 NE Main Street 或 NW 7th Avenue。</p>
<p>最大長度：2 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>State</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>與此位置相關聯的州或省。</p>
<p>最大長度：2 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>StreetName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此位置的街道名稱。</p>
<p>最大長度：60 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>StreetSuffix</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>在街道名稱中指定的街道類型，例如街、道或巷。</p>
<p>最大長度：10 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>UpdateValidationStatus</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>若包括此參數，則會根據是否已透過此 Cmdlet 驗證地址來變更市街地址的 MSAGValid 屬性。如果地址已驗證，MSAGValid 則會設為 True。若省略此參數，MSAGValid 值會保持不變。</p></td>
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

接受含位置資訊伺服器 (LIS) 市街地址物件管線傳送的輸入。

## 傳回類型

這個 Cmdlet 不會傳回值。

## 請參閱

#### 其他資源

[Get-CsLisCivicAddress](get-csliscivicaddress.md)

