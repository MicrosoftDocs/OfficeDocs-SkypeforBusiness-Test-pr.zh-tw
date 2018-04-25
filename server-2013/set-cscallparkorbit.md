---
title: Set-CsCallParkOrbit
TOCTitle: Set-CsCallParkOrbit
ms:assetid: 9a159a9a-69a6-4e4d-8224-49aa42092ea8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398796(v=OCS.15)
ms:contentKeyID: 49291786
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCallParkOrbit

 

_**上次修改主題的時間：** 2015-03-09_

設定組織內現有通話駐留軌道範圍的屬性。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsCallParkOrbit [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsCallParkOrbit [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-CallParkService <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] [-Type <CallPark | GroupPickup>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會將通話駐留範圍 "Redmond CPO 1" 的號碼範圍變更為 500 至 699。在組織內的所有通話駐留範圍之間，此範圍內的所有值必須是唯一的。

    Set-CsCallParkOrbit -Identity "Redmond CPO 1" -NumberRangeStart 500 -NumberRangeEnd 699

## 範例 2

此範例會將通話駐留範圍 "Redmond CPO 2" 的號碼範圍變更為 \*7000 至 \*7100。在組織內的所有通話駐留範圍之間，此範圍內的所有值必須是唯一的。請注意，不同於先前的範例，指派給 NumberRangeStart 和 NumberRangeEnd 的值已括上雙引號。如果這些值的開頭為 \* 或 \# (唯一允許的非數值)，您必須以雙引號括住值。

    Set-CsCallParkOrbit -Identity "Redmond CPO 2" -NumberRangeStart "*7000" -NumberRangeEnd "*7100"

## 詳細描述

保留通話會將接聽的來電指派給特定範圍的號碼以便稍後擷取。通話駐留範圍是針對此目的而定義的一組號碼。**Set-CsCallParkOrbit** Cmdlet 可讓您變更通話駐留服務的號碼範圍及識別碼。在組織內定義的所有通話駐留範圍之間，新的號碼範圍必須是唯一的。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsCallParkOrbit** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCallParkOrbit"}

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
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>主控 通話駐留應用程式 之應用程式服務的完整網域名稱 (FQDN) 或服務識別碼。駐留到 NumberRangeStart 和 NumberRangeEnd 參數所指定之範圍內的號碼的所有通話，將會轉接至此伺服器或集區。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要修改之通話駐留範圍的唯一識別碼。如果 Identity 含有空格，必須以雙引號括住此值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>顯示通話駐留範圍</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。 此物件的類型必須是 DisplayCallParkOrbit，可以透過呼叫 <strong>Get-CsCallParkOrbit</strong> Cmdlet 來擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>NumberRangeEnd</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此通話駐留範圍之範圍中的最後一個號碼。值必須大於或等於 NumberRangeStart。值的長度也必須與 NumberRangeStart 的值相同。例如，如果 NumberRangeStart 設為 100，則 NumberRangeEnd 不可設為 1001。此外，如果 NumberRangeStart 的開頭為 * 或 #，則 NumberRangeEnd 的開頭也必須是相同的字元。</p>
<p>有效值：必須符合規則運算式字串 ([\*|#]?[1-9]\d{0,7})|([1-9]\d{0,8})。這表示值必須是開頭為字元 * 或 # 或數字 1 至 9 的字串 (第一個字元不得為零)。如果第一個字元是 * 或 #，則後續字元必須是數字 1 至 9 (不得為零)。後續字元可以是 0 至 9 的任何數字，最多加上七個字元(例如 &quot;#6000&quot;、&quot;*92000&quot; 以及 &quot;*95551212&quot;)。如果第一個字元不是 * 或 #，則第一個字元必須是數字 1 至 9 (不得為零)，後面最多接著八個字元，每一個字元都是數字 0 至 9 (例如，915551212、41212、300)。</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberRangeStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此通話駐留範圍之範圍中的第一個號碼。值必須小於或等於 NumberRangeEnd。值的長度也必須與 NumberRangeEnd 的值相同。</p>
<p>有效值：必須符合規則運算式字串 ([\*|#]?[1-9]\d{0,7})|([1-9]\d{0,8})。這表示值必須是開頭為字元 * 或 # 或數字 1 至 9 的字串 (第一個字元不得為零)。如果第一個字元是 * 或 #，則後續字元必須是數字 1 至 9 (不得為零)。後續字元可以是 0 至 9 的任何數字，最多加上七個字元(例如 &quot;#6000&quot;、&quot;*92000&quot; 以及 &quot;*95551212&quot;)。* 或 # 的後續數字必須大於 100。如果第一個字元不是 * 或 #，則第一個字元必須是 1 至 9 的數字 (不得為零)，後面加上最多八個字元，每一個字元都是數字 0 至 9 (例如 915551212、41212、300)。</p></td>
</tr>
<tr class="even">
<td><p><em>Type</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Core.OrbitType</p></td>
<td><p>指定通話駐留軌道的類型。Lync Server 2013 允許兩種不同類型的通話駐留軌道︰</p>
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

Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit 物件。接受管線傳送的通話保留範圍物件輸入。

## 傳回類型

此 Cmdlet 會修改 Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit 類型的物件。

## 請參閱

#### 其他資源

[New-CsCallParkOrbit](new-cscallparkorbit.md)  
[Remove-CsCallParkOrbit](remove-cscallparkorbit.md)  
[Get-CsCallParkOrbit](get-cscallparkorbit.md)

