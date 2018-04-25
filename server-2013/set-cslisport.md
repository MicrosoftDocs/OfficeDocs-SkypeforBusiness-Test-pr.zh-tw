---
title: Set-CsLisPort
TOCTitle: Set-CsLisPort
ms:assetid: 8a8a8f95-9366-4d87-bf2a-9767e5eb9996
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398700(v=OCS.15)
ms:contentKeyID: 49291590
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsLisPort

 

_**上次修改主題的時間：** 2015-03-09_

建立位置資訊伺服器 (LIS) 連接埠，關聯連接埠與位置 (若位置不存在，即建立新位置)，或修改現有的連接埠及其關聯位置。增強型 9-1-1 (E9-1-1) Enterprise Voice 實作會利用連接埠與位置之間的關聯，通知緊急服務接線生來電者的位置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsLisPort -ChassisID <String> -PortID <String> [-City <String>] [-CompanyName <String>] [-Country <String>] [-Description <String>] [-HouseNumber <String>] [-HouseNumberSuffix <String>] [-Location <String>] [-PortIDSubType <InterfaceAlias | InterfaceName | LocallyAssigned>] [-PostalCode <String>] [-PostDirectional <String>] [-PreDirectional <String>] [-State <String>] [-StreetName <String>] [-StreetSuffix <String>] <COMMON PARAMETERS>

    Set-CsLisPort -ChassisID <String> -PortID <String> [-Description <String>] [-PortIDSubType <InterfaceAlias | InterfaceName | LocallyAssigned>] <COMMON PARAMETERS>

    Set-CsLisPort -City <String> -CompanyName <String> -Country <String> -HouseNumber <String> -HouseNumberSuffix <String> -Location <String> -PostalCode <String> -PostDirectional <String> -PreDirectional <String> -State <String> -StreetName <String> -StreetSuffix <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會建立或更新 LIS 連接埠位置項目。此範例中的命令包含三個參數：ChassisID、PortID 和 PortIDSubtype。ChassisID 的值為 MAC 位址 99-99-99-99-99-99、PortID 的值為 4200，而 PortIDSubType 的值為 1 (請注意，值為 1 時，PortIDSubType 會轉換為 InterfaceAlias 的值。此參數和值也可以輸入如下：-PortIDSubType InterfaceAlias.)若要建立連接埠位置的唯一執行個體，需要使用這三個參數。

請注意，此範例中不含任何地址資訊。您可以在位置資訊伺服器上建立連接埠項目，而不將該項目與位址產生關聯。不過，透過此連接埠路由傳送的緊急通話可能不會 (端視已經定義的子網路或參數位置而定) 包含緊急服務接線生用來識別位置的足夠資訊。

重要：如果具有此按鍵組合的 LIS 連接埠位置已存在，將會以此命令中的值取代。也就是說，如果此連接埠與某個位址 (實體位置) 相關聯，該關聯性會因為沒有在此命令中加入任何位置資訊而不再存在。此位置仍然存在於位置資料庫中，但不會與此連接埠相關聯。

    Set-CsLisPort -ChassisID 99-99-99-99-99-99 -PortID 4200 -PortIDSubType 1

## 範例 2

範例 2 會透過加入位址資訊來更新在範例 1 中建立的連接埠。如果此位址不存在於位置資料庫中，這個 Cmdlet 就會建立該位置。

    Set-CsLisPort -ChassisID 99-99-99-99-99-99 -PortID 4200 -PortIdSubType 1 -Location "30/1000" -HouseNumber 1234 -PreDirectional NE -StreetName First -StreetSuffix Avenue -City Redmond -State WA -Country US -PostalCode 99999

## 範例 3

這個範例會以 MAC 位址 (ChassisID) 99-99-99-99-99-88 更新針對連接埠定義的所有位置。此範例中的第一行會先呼叫 **Get-CsLisPort** Cmdlet，以擷取已經在 LIS 服務中定義的所有連接埠。接著會將該連接埠集合管線傳送到 **Where-Object** Cmdlet，以尋找集合中 ChassisID 等於 (-eq) 99-99-99-99-99-88 的所有項目。ChassisID 為 99-99-99-99-99-88 的連接埠集合會被指派到變數 $a。

在此範例的第二行中，我們會將變數 $a (ChassisID 為 99-99-99-99-99-88 的 LIS 連接埠集合) 的內容傳送到 **Set-CsLisPort** Cmdlet。這個 Cmdlet 將會取得該集合中的每個項目，並將其更新為指定之參數中的值 (Location、HouseNumber、StreetName、StreetSuffix、City、State、Country 和 PostalCode)。

    $a = Get-CsLisPort | Where-Object {$_.ChassisID -eq "99-99-99-99-99-88"}
    $a | Set-CsLisPort -Location "30/1000" -HouseNumber 1234 -StreetName First -StreetSuffix Avenue -City Redmond -State WA -Country US -PostalCode 99999

## 詳細描述

增強型 9-1-1 讓緊急電話接線生不必詢問來電者的位置資訊，就能找出來電者的位置。當來電者是從 Voice over Internet Protocol (VoIP) 連線撥話時，必須根據各種連線係數來擷取該資訊。VoIP 系統管理員必須設定可判斷來電者位置的位置圖 (稱為線路圖)。這個 Cmdlet 可讓系統管理員將實際位置對應到連接用戶端所使用的連接埠。

ChassisID、PortID 和 PortIDSubType 的組合會變成一個唯一的連接埠位置。如果您輸入已經存在的 ChassisID/PortID/PortIDSubType 按鍵組合，這個 Cmdlet 將會根據所提供的位置參數更新該連接埠的位置。如果此按鍵組合不存在，將會建立一個新的連接埠位置。

如果其位址與此處輸入之位址參數 (包括 null 值) 完全相符的位置不存在於位置資料庫中，就會根據使用此 Cmdlet 輸入的參數建立新的位址 (您可以呼叫 **Get-CsLisLocation** Cmdlet 來擷取位置清單)。**Set-CsLisPort** Cmdlet 不需要位置參數 (或不會提示輸入位置參數)，您可建立沒有與任何位置關聯的連接埠項目。您也可以使用這個 Cmdlet 建立一個無效的位置。有效的位置至少包含 Location (位置)、HouseNumber (門牌號碼)、StreetName (街道名稱)、City (城市)、State (州) 及 Country (國家/地區)。如果您沒有提供所有這些參數，參考之連接埠所收到的呼叫可能不會包含緊急服務接線生所需的資訊 (端視有效的設定是用於參數、子網路或可用來取代連接埠設定的無線存取點而定)。建議您所使用的位置參數盡可能明確，並填入盡可能多的位置參數。

此 Cmdlet 的其中一個必要參數為 ChassisID。ChassisID 是連接埠之網路參數的媒體存取控制 (MAC) 位址。若未指定此參數於位置資料庫中，這個 Cmdlet 就會建立該參數。您可以呼叫 **Get-CsLisSwitch** Cmdlet 來擷取現有的參數。請記住，雖然系統會建立新的交換器項目，但是該交換器不會與使用 **Set-CsLisPort** Cmdlet 輸入的位置資訊自動產生關聯；您必須使用 **Set-CsLisSwitch** Cmdlet 設定交換器位置。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsLisPort** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsLisPort"}

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
<td><p><em>ChassisID</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>連接埠參數的 MAC 位址。這個值必須採用 nn-nn-nn-nn-nn-nn 的格式，例如 12-34-56-78-90-ab，或以 IP 位址表示。如果 ChassisID、PortID 和 PortIDSubType 的組合是唯一的，將會建立新的連接埠位置。如果此組合不是唯一的，具有該按鍵組合的連接埠位置將使用與此命令一起提供的參數值更新。</p></td>
</tr>
<tr class="even">
<td><p><em>PortID</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>與此位置相關聯之連接埠的識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>City</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此連接埠的城市位置。</p>
<p>長度上限：64 個字元。</p></td>
</tr>
<tr class="even">
<td><p><em>CompanyName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此位置的公司名稱。</p>
<p>長度上限：60 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Country</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此連接埠所在的國家/地區。</p>
<p>長度上限：2 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此連接埠位置的詳細說明。</p></td>
</tr>
<tr class="even">
<td><p><em>HouseNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>連接埠位置的門牌號碼。以公司而言，此為公司在街道上的號碼。</p>
<p>最大長度：10 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>HouseNumberSuffix</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>門牌號碼的其他資訊，如 1/2 或 A。例如，1234 1/2 Oak Street 或 1234 A Elm Street。</p>
<p>附註：若要指定公寓號碼或辦公室套房，您必須使用 Location 參數。例如，-Location &quot;Suite 100/Office 150&quot;。</p>
<p>長度上限：5 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>Location</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此位置的名稱。這個值通常是比城市地址更明確的位置名稱 (例如辦公室號碼)，但它可以是任何字串值。</p>
<p>長度上限：20 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>PortIDSubType</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Lis.PortIDSubType</p></td>
<td><p>連接埠的子類型。此值可以輸入為數值或字串，但必須是有效的子類型。有效的子類型為：</p>
<p>1: InterfaceAlias</p>
<p>5: InterfaceName</p>
<p>7: LocallyAssigned</p>
<p>預設值：7 (LocallyAssigned)</p></td>
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

接受管線傳送的 LIS 連接埠物件輸入。

## 傳回類型

此 Cmdlet 會建立或修改 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsLisPort](remove-cslisport.md)  
[Get-CsLisPort](get-cslisport.md)  
[Get-CsLisLocation](get-cslislocation.md)  
[Get-CsLisSwitch](get-cslisswitch.md)

