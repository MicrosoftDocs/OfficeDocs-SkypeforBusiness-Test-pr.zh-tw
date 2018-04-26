---
title: Remove-CsLisLocation
TOCTitle: Remove-CsLisLocation
ms:assetid: 24e49a83-01a9-48ce-b940-fb0503f52077
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425722(v=OCS.15)
ms:contentKeyID: 49290355
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsLisLocation

 

_**上次修改主題的時間：** 2015-03-09_

從增強型 9-1-1 (E9-1-1) 的位置組態資料庫移除位置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsLisLocation [-City <String>] [-CompanyName <String>] [-Country <String>] [-HouseNumber <String>] [-HouseNumberSuffix <String>] [-Location <String>] [-PostalCode <String>] [-PostDirectional <String>] [-PreDirectional <String>] [-State <String>] [-StreetName <String>] [-StreetSuffix <String>] <COMMON PARAMETERS>

    Remove-CsLisLocation -City <String> -CompanyName <String> -Country <String> -HouseNumber <String> -HouseNumberSuffix <String> -Location <String> -PostalCode <String> -PostDirectional <String> -PreDirectional <String> -State <String> -StreetName <String> -StreetSuffix <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會移除名稱為 Bldg30NEWing 的位置。此命令會指定 Location、HouseNumber、StreetName、City、State 以及 Country 參數的值。也就是說，那些是要刪除之位置的唯一屬性 (其中包含非 Null 值)。如果您沒有提供參數值給所有非 Null 的屬性，則不會刪除該位置。系統將會提示您加入尚未在命令中指定的任何參數，但是，如果它們包含 Null 值，只要在每個提示下按 Enter 即可。

    Remove-CsLisLocation -Location Bldg30NEWing -HouseNumber 1000 -StreetName Main -City Redmond -State WA -Country US

## 範例 2

此範例將會移除 LIS 連接埠、子網路、交換器或無線存取點所參考的所有位置。此命令一開始會先呼叫 **Get-CsLisLocation** Cmdlet，並指定 Unreferenced 參數。這將會傳回所有 LIS 連接埠、子網路、交換器或無線存取點沒有參考之位置的集合。接著會將此集合會管線傳送到 **Remove-CsLisLocation** Cmdlet，以移除集合中的每個位置。

    Get-CsLisLocation -Unreferenced | Remove-CsLisLocation

## 詳細描述

E9-1-1 可讓接聽緊急電話的人員判斷來電者的地理位置，而不必詢問來電者該項資訊。在 Lync Server 中，系統是根據對應來電者的連接埠、子網路、交換器或特定位置的無線存取點來判斷位置。此 Cmdlet 會從位置組態資料庫中移除位置。位置的所有屬性會使該位置變成唯一的，因此，您必須輸入該位置的所有非 Null 屬性才能移除。如果您沒有輸入所要移除之位置的所有非 Null 屬性 (而且沒有其他位置僅包含您指定的屬性)，則不會移除任何位置。在此情況下，您不會收到任何錯誤，但是也不會發生任何動作。

此 Cmdlet 將不會移除與位置資訊伺服器 (LIS) 連接埠、子網路、交換器或無線存取點相關聯的位置。如果您嘗試移除這些裝置中任何裝置所參考的位置，將會收到錯誤訊息。您必須先移除所有參考，然後才移除位置。您可以使用 **Remove-CsLisPort** Cmdlet、**Remove-CsLisSubnet** Cmdlet、**Remove-CsLisSwitch** Cmdlet 和 **Remove-CsLisWirelessAccessPoint** Cmdlet 移除這些參考。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsLisLocation** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsLisLocation"}

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
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此位置的城市。</p></td>
</tr>
<tr class="even">
<td><p><em>CompanyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此位置的公司名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>Country</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此位置所在的國家/地區。這個值將包含兩個以下 (含) 的字元。</p></td>
</tr>
<tr class="even">
<td><p><em>HouseNumber</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此位置的門牌號碼。以公司而言，此為公司在街道上的號碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>HouseNumberSuffix</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>門牌號碼的額外資訊，例如 1/2 或 A，舉例來說 1234 1/2 Oak Street 或 1234 A Elm Street。</p></td>
</tr>
<tr class="even">
<td><p><em>Location</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此位置的名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>PostalCode</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>與此位置相關聯的郵遞區號。</p></td>
</tr>
<tr class="even">
<td><p><em>PostDirectional</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>街道名稱的方向指定。例如，Main Street NE 或 7th Avenue NW 中的 NE 或 NW。</p></td>
</tr>
<tr class="odd">
<td><p><em>PreDirectional</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>在街道名稱之前的街道名稱方向指定。例如 NE 或 NW 代表 NE Main Street 或 NW 7th Avenue。</p></td>
</tr>
<tr class="even">
<td><p><em>State</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>與此位置相關聯的省或市。此值將是兩個以下 (含) 的字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>StreetName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此位置的街道名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>StreetSuffix</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>街道名稱中指定的街道類型，例如 Street、Avenue 或 Court。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

接受管線傳送的 LIS 位置物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值或物件，而會移除 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Set-CsLisLocation](set-cslislocation.md)  
[Get-CsLisLocation](get-cslislocation.md)  
[Remove-CsLisPort](remove-cslisport.md)  
[Remove-CsLisSubnet](remove-cslissubnet.md)  
[Remove-CsLisSwitch](remove-cslisswitch.md)  
[Remove-CsLisWirelessAccessPoint](remove-csliswirelessaccesspoint.md)  
[Get-CsLisCivicAddress](get-csliscivicaddress.md)

