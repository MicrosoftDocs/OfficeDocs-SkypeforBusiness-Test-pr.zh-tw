---
title: Set-CsLisWirelessAccessPoint
TOCTitle: Set-CsLisWirelessAccessPoint
ms:assetid: 9c491f8d-c4c0-48e5-afc2-0153864dab41
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412723(v=OCS.15)
ms:contentKeyID: 49291802
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsLisWirelessAccessPoint

 

_**上次修改主題的時間：** 2015-03-09_

建立位置資訊伺服器 (LIS) 無線存取點 (WAP)，關聯 WAP 與位置 (若位置不存在，即建立新位置)，或修改現有的 WAP 及其關聯位置。增強型 9-1-1 (E9-1-1) Enterprise Voice 實作會利用 WAP 與位置之間的關聯，通知緊急服務接線生來電者的位置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsLisWirelessAccessPoint -BSSID <String> [-City <String>] [-CompanyName <String>] [-Country <String>] [-Description <String>] [-HouseNumber <String>] [-HouseNumberSuffix <String>] [-Location <String>] [-PostalCode <String>] [-PostDirectional <String>] [-PreDirectional <String>] [-State <String>] [-StreetName <String>] [-StreetSuffix <String>] <COMMON PARAMETERS>

    Set-CsLisWirelessAccessPoint -BSSID <String> [-Description <String>] <COMMON PARAMETERS>

    Set-CsLisWirelessAccessPoint -City <String> -CompanyName <String> -Country <String> -HouseNumber <String> -HouseNumberSuffix <String> -Location <String> -PostalCode <String> -PostDirectional <String> -PreDirectional <String> -State <String> -StreetName <String> -StreetSuffix <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會建立或更新 LIS WAP 位置項目。此範例中的命令只包含一個 (必要) 參數：BSSID。BSSID 的值是 WAP 的 Identifier (使用 MAC 位址的格式)，在此範例中為 99-99-99-99-99-99。

請注意，此範例不包含任何位址資訊。您可以在位置資訊伺服器上建立 WAP 項目，而不將該項目與位址產生關聯。不過，透過此 WAP 路由傳送的緊急電話可能不包含供緊急服務接線生識別位置所需的足夠資訊。

重要：如果具有此 BSSID 的 LIS WAP 位置已經存在，將會以此命令中的值取代。也就是說，如果此 WAP 與某個位址 (實體位置) 相關聯，該關聯性會因為沒有在此命令中加入任何位置資訊而不再存在。此位置仍然存在於位置資料庫中，但不會與此 WAP 相關聯。

    Set-CsLisWirelessAccessPoint -BSSID 99-99-99-99-99-99

## 範例 2

範例 2 會透過加入位址資訊來更新在範例 1 中建立的 WAP (這會實際刪除現有的項目，並以此新項目取代)。如果此位址不存在於位置資料庫中，這個 Cmdlet 就會建立該位置。

    Set-CsLisWirelessAccessPoint -BSSID 99-99-99-99-99-99 -Location "30/1000" -HouseNumber 1234 -PreDirectional NE -StreetName First -StreetSuffix Avenue -City Redmond -State WA -Country US -PostalCode 99999

## 詳細描述

增強型 9-1-1 讓緊急電話接線生不必詢問來電者的位置資訊，就能找出來電者的位置。當來電者是從 Voice over Internet Protocol (VoIP) 連線撥話時，必須根據各種連線係數來擷取該資訊。VoIP 系統管理員必須設定可判斷來電者位置的位置圖 (稱為線路圖)。這個 Cmdlet 可讓系統管理員將實際位置對應到路由傳送來電所使用的 WAP。

BSSID 參數是此 Cmdlet 的唯一必要參數。如果您輸入已經存在的 BSSID 值，這個 Cmdlet 將會根據所提供的位置參數更新該 WAP 的位置。如果 BSSID 不存在，則會建立新的 WAP 位置。

如果其位址與此處輸入之位址參數 (包括 null 值) 完全相符的位置不存在於位置資料庫中，就會根據使用此 Cmdlet 輸入的參數建立新的位址 (您可以呼叫 **Get-CsLisLocation** Cmdlet 來擷取位置清單)。**Set-CsLisWirelessAccessPoint** Cmdlet 不需要也不會提示位置參數，因此您可以建立一個 WAP 項目，而不將該項目與位置產生關聯。您也可以使用這個 Cmdlet 建立一個無效的位置。有效的位置至少包含 Location (位置)、HouseNumber (門牌號碼)、StreetName (街道名稱)、City (城市)、State (州) 及 Country (國家/地區)。如果您未提供以上所有參數，則由所參考之 WAP 接聽的來電可能就不包含緊急服務接線生需要的資訊。建議您所使用的位置參數盡可能明確，並填入盡可能多的位置參數。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsLisWirelessAccessPoint** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsLisWirelessAccessPoint"}

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
<td><p>無線存取點的基礎服務組識別元 (BSSID)。這個值必須採用 nn-nn-nn-nn-nn-nn 的格式，例如 12-34-56-78-90-ab。如果具有指定之 BSSID 值的項目不存在，則會建立新的 WAP 位置。如果具有指定之 BSSID 的項目存在，則會取代該項目。</p></td>
</tr>
<tr class="even">
<td><p><em>City</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此位置的城市。</p>
<p>長度上限：64 個字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>CompanyName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此位置的公司名稱。</p>
<p>長度上限：60 個字元</p></td>
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
<p>長度上限：2 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此 WAP 位置的詳細說明。</p></td>
</tr>
<tr class="odd">
<td><p><em>HouseNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此位置的門牌號碼。以公司而言，此為公司在街道上的號碼。</p>
<p>最大長度：10 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>HouseNumberSuffix</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>門牌號碼的其他資訊，如 1/2 或 A。例如，1234 1/2 Oak Street 或 1234 A Elm Street。</p>
<p>注意：若要指定公寓號碼或辦公室套房，您必須使用 Location 參數。例如，-Location &quot;Suite 100/Office 150&quot;。</p>
<p>長度上限：5 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>Location</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此位置的名稱。這個值通常是比城市地址更明確的位置名稱 (例如辦公室號碼)，但它可以是任何字串值。</p>
<p>長度上限：20 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>PostalCode</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>與此位置相關聯的郵遞區號。</p>
<p>長度上限：10 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>PostDirectional</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>街道名稱的方向指定。例如，Main Street NE 或 7th Avenue NW 中的 NE 或 NW。</p>
<p>長度上限：2 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>PreDirectional</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>在街道名稱之前的街道名稱方向指定。例如 NE 或 NW 代表 NE Main Street 或 NW 7th Avenue。</p>
<p>最大長度：2 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>State</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>與此位置相關聯的省或市。</p>
<p>長度上限：2 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>StreetName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此位置的街道名稱。</p>
<p>長度上限：60 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>StreetSuffix</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>街道名稱中指定的街道類型，例如 Street、Avenue 或 Court。</p>
<p>長度上限：10 個字元</p></td>
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

接受管線傳送的 LIS 無線存取點物件輸入。

## 傳回類型

此 Cmdlet 會建立或修改 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsLisWirelessAccessPoint](remove-csliswirelessaccesspoint.md)  
[Get-CsLisWirelessAccessPoint](get-csliswirelessaccesspoint.md)  
[Get-CsLisLocation](get-cslislocation.md)

