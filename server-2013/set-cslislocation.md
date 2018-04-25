---
title: Set-CsLisLocation
TOCTitle: Set-CsLisLocation
ms:assetid: 955cdce0-250d-48b7-8891-5355d801911f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398757(v=OCS.15)
ms:contentKeyID: 49291707
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsLisLocation

 

_**上次修改主題的時間：** 2015-03-09_

在增強型 9-1-1 (E9-1-1) 的位置組態資料庫中建立新的位置或修改現有的位置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsLisLocation -Instance <PSObject> [-City <String>] [-CompanyName <String>] [-Country <String>] [-HouseNumber <String>] [-HouseNumberSuffix <String>] [-Location <String>] [-PostalCode <String>] [-PostDirectional <String>] [-PreDirectional <String>] [-State <String>] [-StreetName <String>] [-StreetSuffix <String>] <COMMON PARAMETERS>

    Set-CsLisLocation -City <String> -CompanyName <String> -Country <String> -HouseNumber <String> -HouseNumberSuffix <String> -Location <String> -PostalCode <String> -PostDirectional <String> -PreDirectional <String> -State <String> -StreetName <String> -StreetSuffix <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會建立名為 Bldg30NEWing 的新位置。此命令會填寫所有必要參數，以便有值可用來建立位置。在此範例中，位置的地址為 1000 Main, Redmond, WA, US。輸入該地址的方法為以值 1000 指定 HouseNumber 參數、以值 Main 指定 StreetName 參數、以值 Redmond 指定 City 參數，並以值 US 指定 Country 參數。

請注意，如果您只使用此處顯示的參數來執行命令，系統將提示您輸入其他參數。不過，您可以在每個提示出現時直接按 Enter 鍵，而不提供值，即可建立位置。

    Set-CsLisLocation -Location Bldg30NEWing -HouseNumber 1000 -StreetName Main -City Redmond -State WA -Country US

## 範例 2

此範例和範例 1 一樣會建立新的位置。然而，此範例中的命令會指定 Cmdlet 的所有參數。這樣將可避免出現範例 1 的命令所引起的提示，因為此範例會直接將任何我們想要留空的值設定成空字串。

    Set-CsLisLocation -Location "Suite 100/Office 20" -CompanyName "Litware, Inc." -HouseNumber 1234 -HouseNumberSuffix "" -PreDirectional "" -StreetName Main -StreetSuffix St -PostDirectional "" -City Redmond -State WA -PostalCode 99999 -Country US

## 範例 3

此範例會修改範例 1 中建立的位置。範例中的第一行會先呼叫 **Get-CsLisLocation** Cmdlet，這會傳回 Lync Server 部署內所定義之所有位置的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會從集合中擷取 Location 屬性等於 (-ceq，區分大小寫的等於) Bldg30NEWing 的所有項目。符合此準則的物件會指派給 $a 變數。

在第 2 行，我們呼叫 **Set-CsLisLocation** Cmdlet。第一個參數為 Instance 參數。我們將包含在第 1 行擷取之物件的變數 ($a) 傳遞給此參數，此物件正好是我們想要修改的物件。然後，我們指定 StreetSuffix 參數並傳遞 Street 值給它。這會將變數 $a 中位置的 StreetSuffix 屬性值變更為 Street。

請注意，因為 Location 不是唯一屬性，所以 **Where-Object** Cmdlet 可能會傳回多個位置。若是如此，此範例將無法運作。若要一次修改多個位置，請參閱範例 4。

    $a = Get-CsLisLocation | Where-Object {$_.Location -ceq "Bldg30NEWing"}
    Set-CsLisLocation -Instance $a -StreetSuffix Street

## 範例 4

範例 4 會修改一或多個位置物件的 StreetSuffix 屬性。此範例的開頭很像範例 3。我們會先呼叫 **Get-CsLisLocation** Cmdlet 擷取所有位置。接著，將此位置集合管線傳送至 **Where-Object** Cmdlet，以將集合縮小到只有 Location 屬性等於 NorthCampus 的位置。此新的集合會儲存於變數 $a 中。在第 2 行，我們將 $a 的內容管線傳送至 **Set-CsLisLocation** Cmdlet。此 Cmdlet 會逐一處理 $a 中所儲存的每個物件 (每個位置)，並修改該物件。此處所指的修改是將每個物件的 StreetSuffix 屬性變更為 Avenue。

此範例中的命令不使用變數也能完成。只需將 **Where-Object** Cmdlet 的結果管線傳送至 **Set-CsLisLocation** Cmdlet 即可，如下所示：

Get-CsLisLocation | Where-Object {$\_.Location -ceq "NorthCampus"} | Set-CsLisLocation -StreetSuffix Avenue

    $a = Get-CsLisLocation | Where-Object {$_.Location -ceq "NorthCampus"}
    $a | Set-CsLisLocation -StreetSuffix Avenue

## 詳細描述

E9-1-1 可讓接聽緊急電話的人能夠判斷來電者的地理位置，而無須向來電者詢問該資訊。在 Lync Server 中，系統是根據對應來電者的連接埠、子網路、交換器或特定位置的無線存取點來判斷位置 (此對應稱為連線對應)。此 Cmdlet 會在位置資訊伺服器 (LIS) 上之位置組態資料庫中所儲存的位置清單中，新增地址或修改現有地址。這些位置後續會對應到與公司合作之緊急服務提供者所提供的有效地址清單。

此 Cmdlet 所有必要參數 (Instance 除外) 的組合會構成唯一的項目。變更其中任何參數都將建立新的位置，而不是修改現有的位置。請注意，雖然這些參數全都是必要參數，但是有些參數可能包含 Null 值。必須包含非 Null 值的參數為：Location、HouseNumber、StreetName、City、State 和 Country。若要變更現有值，您必須使用 Instance 參數 (或將執行個體傳送至 Cmdlet)。

除了可使用此 Cmdlet 建立位置外，針對連接埠、子網路、交換器或無線存取點資訊輸入新地址時，也會自動建立位置。您可以使用 **Set-CsLisPort** Cmdlet、**Set-CsLisSubnet** Cmdlet、**Set-CsLisSwitch** Cmdlet 和 **Set-CsLisWirelessAccessPoint** Cmdlet 來輸入此資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsLisLocation** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsLisLocation"}

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
<td><p>城市位置。</p>
<p>最大長度：64 個字元。</p></td>
</tr>
<tr class="even">
<td><p><em>CompanyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此位置之公司的名稱。</p>
<p>最大長度：60 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>Country</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此位置所在國家/地區。</p>
<p>最大長度：2 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>HouseNumber</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>位置的門牌號碼。以公司而言，此為公司在街道上的號碼。</p>
<p>最大長度：10 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>HouseNumberSuffix</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>門牌號碼的額外資訊，例如 1/2 或 A，舉例來說 1234 1/2 Oak Street 或 1234 A Elm Street。</p>
<p>附註：若要指定公寓門號或辦公室房間，您必須使用 Location 參數。例如 -Location &quot;Suite 100/Office 150&quot;。</p>
<p>最大長度：5 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>必要</p></td>
<td><p>PSObject</p></td>
<td><p>位置物件的參考。此物件必須包含建立位置所需的屬性。您可以呼叫 <strong>Get-CsLisLocation</strong> Cmdlet 來擷取此類型的物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>Location</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此位置的名稱。通常，這個值是比街道地址更明確的名稱 (例如辦公室號碼)，但是可以是任何字串值。</p>
<p>最大長度：20 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>PostalCode</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>與此位置關聯的郵遞區號。</p>
<p>最大長度：10 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>PostDirectional</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>街道名稱的方向指定。例如 NE 或 NW 代表 Main Street NE 或 7th Avenue NW。</p>
<p>最大長度：2 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>PreDirectional</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>街道名稱的方向指定放在街道名稱前。例如 NE 或 NW 代表 NE Main Street 或 NW 7th Avenue。</p>
<p>最大長度：2 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>State</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>與此位置相關聯的州或省。</p>
<p>最大長度：2 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>StreetName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此位置的街道名稱。</p>
<p>最大長度：60 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>StreetSuffix</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>在街道名稱中指定的街道類型，例如街、道或巷。</p>
<p>最大長度：10 個字元</p></td>
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

接受管線傳送的 LIS 位置物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值或物件，而會建立或修改 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsLisLocation](remove-cslislocation.md)  
[Get-CsLisLocation](get-cslislocation.md)  
[Set-CsLisPort](set-cslisport.md)  
[Set-CsLisSubnet](set-cslissubnet.md)  
[Set-CsLisSwitch](set-cslisswitch.md)  
[Set-CsLisWirelessAccessPoint](set-csliswirelessaccesspoint.md)  
[Get-CsLisCivicAddress](get-csliscivicaddress.md)

