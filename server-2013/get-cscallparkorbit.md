---
title: Get-CsCallParkOrbit
TOCTitle: Get-CsCallParkOrbit
ms:assetid: 73bbb09a-7966-4af1-aff3-001f5cc56df1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398554(v=OCS.15)
ms:contentKeyID: 49291328
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCallParkOrbit

 

_**上次修改主題的時間：** 2015-03-09_

取得組織的通話駐留範圍設定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsCallParkOrbit [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsCallParkOrbit [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Type <CallPark | GroupPickup>]

## 範例

## 範例 1

此範例會呼叫不含其他任何參數的 **Get-CsCallParkOrbit** Cmdlet。以這種方式呼叫時，**Get-CsCallParkOrbit** Cmdlet 會傳回設定供組織使用之所有通話駐留範圍的集合。

    Get-CsCallParkOrbit

## 範例 2

範例 2 會使用 **Get-CsCallParkOrbit** Cmdlet 傳回名為 "Redmond CPO 1" 之通話駐留範圍的資訊。

    Get-CsCallParkOrbit -Identity "Redmond CPO 1"

## 範例 3

此範例中的命令會傳回 Identity 中含有 "Redmond" 字串的所有通話駐留範圍。例如，此命令會傳回識別身分為 "Redmond 501"、"CP Redmond 1" 和 "ARedmond" 等的通話駐留範圍。此命令使用 Filter 參數和萬用字元 (\*) 來指定搜尋目標 (此搜尋不區分大小寫)。

    Get-CsCallParkOrbit -Filter *Redmond*

## 範例 4

此命令會傳回指派給識別碼為 ApplicationServer:pool0.litwareinc.com 之通話駐留服務的所有通話駐留範圍。**Get-CsCallParkOrbit** Cmdlet 會擷取所有通話駐留範圍的集合，然後，此集合會管線傳送到 **Where-Object** Cmdlet。此 **Where-Object** Cmdlet 呼叫會在該集合中尋找 CallParkServiceId 屬性的值為 ApplicationServer:pool0.litwareinc.com 的所有通話駐留範圍。請注意，我們在 CallParkServiceId 參數名稱的尾端加入 toString 方法。CallParkServiceId 屬於 WritableServiceId 類型。為了將該值與提供的字串比較，我們必須呼叫 toString 方法，藉此先將其轉為字串。

    Get-CsCallParkOrbit | Where-Object {$_.CallParkServiceId.toString() -eq "ApplicationServer:pool0.litwareinc.com"}

## 範例 5

此範例中的命令會傳回號碼範圍開頭為 \* 首碼的所有通話駐留範圍。在 **Get-CsCallParkOrbit** Cmdlet 擷取所有通話駐留範圍的集合之後，接著會將該集合管線傳送給 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會將集合縮減至通話駐留位置開頭為 \* 的通話駐留範圍。作法為檢查 NumberRangeStart 物件的 StartsWith 屬性是否包含 "\*" 字串。

    Get-CsCallParkOrbit | Where-Object {$_.NumberRangeStart.StartsWith("*")}

## 範例 6

此範例中的命令會傳回未指派首碼給範圍中號碼的所有通話駐留範圍。(首碼是指置於號碼開頭的 \* 或 \# 值)。此命令傳回的所有通話駐留範圍是只含數字、不含其他任何字元的範圍。**Get-CsCallParkOrbit** Cmdlet 會擷取所有通話駐留範圍的集合，然後將該集合管線傳送給 **Where-Object** Cmdlet。查看 **Where-Object** Cmdlet 呼叫中的準則，我們可以看到：$\_.NumberRangeStart\[0\])。這會傳回範圍開頭號碼的第一個字元 (請注意，我們只需要檢查範圍的開頭︰如果範圍中的起始號碼沒有首碼，則結束號碼也不會有。) 此字元會傳遞給 IsDigit 函式，以判斷是否為數值字元。如果是的話，則會傳回相對應集合項目的通話駐留範圍資訊。

    Get-CsCallParkOrbit | Where-Object {[Char]::IsDigit($_.NumberRangeStart[0])}

## 詳細描述

此 Cmdlet 會擷取針對組織定義之通話駐留範圍的設定。您可以擷取單一通話駐留範圍 (以 Identity 參數指定)，也可以呼叫不含參數的 **Get-CsCallParkOrbit** Cmdlet，以擷取針對組織定義的所有通話駐留範圍。通話駐留範圍的組成設定會指定使用者可以駐留通話的號碼範圍，以及與這些號碼範圍相關聯的伺服器。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsCallParkOrbit** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmin。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCallParkOrbit"}

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此參數接受萬用字元字串，並傳回識別身分符合該字串的所有通話駐留範圍。例如，Filter 值為 Redmond* 會傳回名稱開頭為 Redmond 字串的所有通話駐留範圍，例如 Redmond 1、Redmond 2 和 RedmondCPO 等。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>通話駐留範圍的唯一名稱。此名稱由系統管理員在定義通話保留範圍時指派。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取通話保留範圍資訊，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Type</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Core.OrbitType</p></td>
<td><p>指定要擷取之通話駐留軌道的類型。Lync Server 2013 允許兩種不同類型的通話駐留軌道︰</p>
<p>CallPark。這是標準的通話駐留軌道，使用者保留通話後，可以從任何電話上撥打指定的通話駐留號碼，即可擷取該通話。</p>
<p>GroupPickup。如為群組接聽，使用者可以接聽任何撥打給所屬來電接聽群組中任何成員的來電。來電接聽群組是由系統管理員所設定。</p>
<p>若要傳回指定類型的通話駐留軌道，請使用類似下列的語法︰</p>
<p>-Type GroupPickup</p>
<p>若要傳回所有通話駐留軌道，不論類型為何，只需省略 Type 參數。</p>
<p>此參數已在 Lync Server 2013 的 2013 年 2 月版本中導入。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

此 Cmdlet 會傳回 Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbits 類型的物件

## 請參閱

#### 其他資源

[New-CsCallParkOrbit](new-cscallparkorbit.md)  
[Remove-CsCallParkOrbit](remove-cscallparkorbit.md)  
[Set-CsCallParkOrbit](set-cscallparkorbit.md)

