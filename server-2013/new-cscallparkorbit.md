---
title: New-CsCallParkOrbit
TOCTitle: New-CsCallParkOrbit
ms:assetid: d65a000f-905d-4512-b082-066748719f4c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398936(v=OCS.15)
ms:contentKeyID: 49292474
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsCallParkOrbit

 

_**上次修改主題的時間：** 2015-03-09_

建立新的具名號碼範圍，以指派給組織中的駐留通話。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsCallParkOrbit -Identity <XdsGlobalRelativeIdentity> -CallParkService <String> -NumberRangeEnd <String> -NumberRangeStart <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Type <CallPark | GroupPickup>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

這個範例會在服務識別碼為 ApplicationServer:pool0.litwareinc.com 的應用程式伺服器上建立名為 "Redmond CPO 1" 的新通話駐留範圍。這個通話駐留範圍的可用號碼範圍為 100 到 199。

    New-CsCallParkOrbit -Identity "Redmond CPO 1" -NumberRangeStart 100 -NumberRangeEnd 199 -CallParkService ApplicationServer:pool0.litwareinc.com

## 範例 2

這個範例會在 FQDN 為 pool0.litwareinc.com 的通話保留應用程式伺服器上建立名為 "Redmond CPO 2" 的新通話保留範圍。這個通話保留範圍的可用範圍為 \*1000 到 \*1999。

    New-CsCallParkOrbit -Identity "Redmond CPO 2" -NumberRangeStart "*1000" -NumberRangeEnd "*1999" -CallParkService pool0.litwareinc.com

## 範例 3

這個範例會在服務識別碼為 ApplicationServer:redmond.litwareinc.com 的通話駐留應用程式伺服器上建立名為 "Redmond CPO 3" 的新通話駐留範圍。這個通話駐留範圍的可用範圍為 \#1000 到 \#1999。

    New-CsCallParkOrbit -Identity "Redmond CPO 3" -NumberRangeStart "#1000" -NumberRangeEnd "#1999"  -CallParkService ApplicationServer:redmond.litwareinc.com

## 詳細描述

保留通話會將接聽的來電指派給特定號碼以便稍後擷取。通話駐留範圍是針對此目的而指派給特定通話駐留服務的一組通話駐留位置。**New-CsCallParkOrbit** Cmdlet 會定義通話駐留範圍的號碼，並將其套用到特定的服務。在指定的範圍中保留的通話會保留在指定的通話駐留服務中。您可以建立多個通話保留範圍，每個範圍都必須具備一個全域唯一名稱和唯一的號碼範圍。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsCallParkOrbit** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsCallParkOrbit"}

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
<td><p><em>CallParkService</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>主控 通話駐留應用程式 之應用程式服務的完整網域名稱 (FQDN) 或服務識別碼。保留給 NumberRangeStart 和 NumberRangeEnd 參數所指定之範圍內的號碼的所有通話，將會轉接至此伺服器或集區。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>通話駐留範圍的名稱。這個名稱在 Lync Server 部署中必須是唯一的。這個字串可以是任何值，但是應該能夠很容易識別特定的通話駐留範圍。所有通話駐留範圍都以全域範圍建立。</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberRangeEnd</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此通話保留範圍中的最後一個號碼。值必須大於或等於 NumberRangeStart。值的長度也必須與 NumberRangeStart 的值相同。例如，如果 NumberRangeStart 設為 100，則 NumberRangeEnd 不能設為 1001。此外，如果 NumberRangeStart 的開頭為 * 或 #，則 NumberRangeEnd 的開頭必須為相同的字元。</p>
<p>有效值：必須符合規則運算式字串 ([\*|#]?[1-9]\d{0,7})|([1-9]\d{0,8})。這表示值必須是開頭為字元 * 或 # 或數字 1 至 9 的字串 (第一個字元不得為零)。如果第一個字元是 * 或 #，則後續字元必須是數字 1 至 9 (不得為零)。後續字元可以是 0 至 9 的任何數字，最多加上七個字元 (例如，#6000、*92000 及 *95551212)。如果第一個字元不是 * 或 #，則第一個字元必須是數字 1 至 9 (不得為零)，後面最多接著八個字元，每一個字元都是數字 0 至 9 (例如：915551212;41212;300)</p></td>
</tr>
<tr class="even">
<td><p><em>NumberRangeStart</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此通話保留範圍中的第一個號碼。值必須小於或等於 NumberRangeEnd。值的長度也必須與 NumberRangeEnd 的值相同。</p>
<p>有效值：必須符合規則運算式字串 ([\*|#]?[1-9]\d{0,7})|([1-9]\d{0,8})。這表示值必須是開頭為字元 * 或 # 或數字 1 至 9 的字串 (第一個字元不得為零)。如果第一個字元是 * 或 #，則後續字元必須是數字 1 至 9 (不得為零)。後續字元可以是 0 至 9 的任何數字，最多加上七個字元 (例如，#6000、*92000 及 *95551212)。* 或 # 之後的號碼必須大於 100。如果第一個字元不是 * 或 #，則第一個字元必須是數字 1 到 9 (不得為零)，後面最多接著八個字元，每一個字元都是數字 0 至 9 (例如，915551212;41212;300)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>Type</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Core.OrbitType</p></td>
<td><p>指定要建立之通話駐留軌道的類型。Lync Server 2013 允許兩種不同類型的通話駐留軌道︰</p>
<p>CallPark。這是標準的通話駐留軌道，使用者保留通話後，可以從任何電話上撥打指定的通話駐留號碼，即可擷取該通話。CallPark 是預設的軌道類型，會在未指定 Type 參數時使用。</p>
<p>GroupPickup。如為群組接聽，使用者可以接聽任何撥打給所屬來電接聽群組中任何成員的來電。來電接聽群組是由系統管理員所設定。</p>
<p>若要指定通話駐留軌道類型，請使用類似下列的語法︰</p>
<p>-Type GroupPickup</p>
<p>此參數已在 Lync Server 2013 的 2013 年 2 月版本中導入。</p></td>
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

無。

## 傳回類型

此 Cmdlet 會建立 Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsCallParkOrbit](remove-cscallparkorbit.md)  
[Set-CsCallParkOrbit](set-cscallparkorbit.md)  
[Get-CsCallParkOrbit](get-cscallparkorbit.md)

