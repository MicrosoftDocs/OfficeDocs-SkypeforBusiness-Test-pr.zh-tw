---
title: Set-CsLisSubnet
TOCTitle: Set-CsLisSubnet
ms:assetid: e51ef9ec-c307-4046-b64b-f23b354713fc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399016(v=OCS.15)
ms:contentKeyID: 49292618
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsLisSubnet

 

_**上次修改主題的時間：** 2015-03-09_

建立位置資訊伺服器 (LIS) 子網路，關聯子網路與位置 (若位置不存在，即建立新位置)，或修改現有的子網路及其關聯位置。增強型 9-1-1 (E9-1-1) Enterprise Voice 實作會利用子網路與位置之間的關聯，通知緊急服務接線生來電者的位置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsLisSubnet -Subnet <String> [-Description <String>] <COMMON PARAMETERS>

    Set-CsLisSubnet -Subnet <String> [-City <String>] [-CompanyName <String>] [-Country <String>] [-Description <String>] [-HouseNumber <String>] [-HouseNumberSuffix <String>] [-Location <String>] [-PostalCode <String>] [-PostDirectional <String>] [-PreDirectional <String>] [-State <String>] [-StreetName <String>] [-StreetSuffix <String>] <COMMON PARAMETERS>

    Set-CsLisSubnet -City <String> -CompanyName <String> -Country <String> -HouseNumber <String> -HouseNumberSuffix <String> -Location <String> -PostalCode <String> -PostDirectional <String> -PreDirectional <String> -State <String> -StreetName <String> -StreetSuffix <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會建立或更新 LIS 子網路位置項目。此範例中的命令只包含一個 (必要) 參數：Subnet。此範例中的 Subnet 值為 IPv4 位址，192.10.10.0。

請注意，此範例中不含任何地址資訊。在位置資訊伺服器上有可能建立沒有與任何地址關聯的子網路項目。但是，透過此子網路路由的緊急電話包含的資訊可能不夠 (根據已定義的交換器或連接埠位置而定) 供緊急接線生辨識位置。

重要：如果已存在此 Subnet 值的 LIS 子網路位置，會被此命令中的值取代。也就是說，如果此子網路與某個地址 (實際位置) 相關聯，此關聯將不再存在，因為命令中並未加入任何位置資訊。此位置仍會繼續存在位置資料庫中，但不再與此子網路有關聯。

    Set-CsLisSubnet -Subnet 192.10.10.0

## 詳細描述

增強型 9-1-1 讓緊急電話接線生不必詢問來電者的位置資訊，就能找出來電者的位置。當來電者是從 Voice over Internet Protocol (VoIP) 連線撥話時，必須根據各種連線係數來擷取該資訊。VoIP 系統管理員必須設定位置對應圖 (稱做接線圖) 來判定來電者的的位置。此 Cmdlet 讓系統管理員可以將實際位置對應到用戶端連線所透過的子網路。

Subnet 參數是這個 Cmdlet 唯一需要的參數。如果您輸入已存在的 Subnet 值，此 Cmdlet 將會根據所提供的位置參數更新該子網路的位置。如果 Subnet 不存在，則會建立新的子網路位置。

如果在位置資料庫沒有任何位置的位址符合此處輸入的位址參數 (包括 null 值)，會根據此 Cmdlet 的輸入參數建立新位址 (您可以呼叫 **Get-CsLisLocation** Cmdlet 來擷取位置清單)。**Set-CsLisSubnet** Cmdlet 不需要位置參數 (或不會提示輸入位置參數)，您可建立沒有與任何位置關聯的子網路項目。使用此 Cmdlet 也可能建立無效的位置。有效的位置至少包含 Location (位置)、HouseNumber (門牌號碼)、StreetName (街道名稱)、City (城市)、State (州) 及 Country (國家/地區)。如果您並未提供所有這些參數，則源自指定子網路的呼叫可能不會包含緊急總機所需的資訊 (視有效設定是否可用於交換器、連接埠或可用於子網路設定處的無線存取點而定)。建議您位置參數盡可能填寫且盡可能詳細。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsLisSubnet** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsLisSubnet"}

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
<td><p><em>Subnet</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>子網路的 IP 位址。此值必須輸入為 IPv4 位址 (以點區隔位數，例如 192.0.2.0)。</p></td>
</tr>
<tr class="even">
<td><p><em>City</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>城市位置。</p>
<p>最大長度：64 個字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>CompanyName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此位置之公司的名稱。</p>
<p>最大長度：60 個字元</p></td>
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
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>這個子網路位置的詳細說明。</p></td>
</tr>
<tr class="odd">
<td><p><em>HouseNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>位置的門牌號碼。以公司而言，此為公司在街道上的號碼。</p>
<p>最大長度：10 個字元</p></td>
</tr>
<tr class="even">
<td><p><em>HouseNumberSuffix</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>門牌號碼的額外資訊，例如 1/2 或 A，舉例來說 1234 1/2 Oak Street 或 1234 A Elm Street。</p>
<p>附註：若要指定公寓門號或辦公室房間，您必須使用 Location 參數。例如 -Location &quot;Suite 100/Office 150&quot;。</p>
<p>最大長度：5 個字元</p></td>
</tr>
<tr class="odd">
<td><p><em>Location</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此位置的名稱。通常，這個值是比街道地址更明確的名稱 (例如辦公室號碼)，但是可以是任何字串值。</p>
<p>最大長度：20 個字元</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

接受 LIS 子網路物件的管線傳送資料。

## 傳回類型

此 Cmdlet 會建立或修改 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsLisSubnet](remove-cslissubnet.md)  
[Get-CsLisSubnet](get-cslissubnet.md)  
[Get-CsLisLocation](get-cslislocation.md)

