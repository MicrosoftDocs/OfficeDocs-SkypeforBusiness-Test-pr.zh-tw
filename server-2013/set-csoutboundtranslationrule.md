---
title: Set-CsOutboundTranslationRule
TOCTitle: Set-CsOutboundTranslationRule
ms:assetid: fbf82146-7884-418c-8239-66c0ca0f2ba6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413073(v=OCS.15)
ms:contentKeyID: 49292909
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsOutboundTranslationRule

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的外撥轉譯規則。外撥轉譯規則會將電話號碼轉換成當地的撥號格式，以與專用交換機 (PBX) 系統互動。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsOutboundTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsOutboundTranslationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會修改 Identity 為 site:Redmond/Prefix Redmond 的全域外撥轉譯規則。我們包含了一個 Description，說明此規則適合用來將數字從 E.164 格式轉譯為七位數字的電話號碼。此外，還會指定 Pattern 和 Translation 值，這將會修改這些屬性的現有值。這些值會將利用規則運算式以 Pattern 指定的 E.164 號碼 (在此範例中是以 +1425 開頭的 12 位數字) 移去前面 5 個數字，轉譯為 7 位數字。例如，號碼 +14255551212 將轉譯為號碼 5551212。

    Set-CsOutboundTranslationRule -Identity "site:Redmond/Prefix Redmond" -Description "Convert to seven digits" -Pattern '^\+1425(\d{7})$' -Translation '$1'

## 範例 2

此範例會修改外撥轉譯規則的 Name 屬性。請注意，這樣會變更此規則的 Identity。此範例的第一個命令是呼叫 **Get-CsOutboundTranslationRule** Cmdlet。我們將 Identity 指定為 site:Redmond\\OBR1，它將傳回一個轉譯規則，已指定 Identity 的規則。我們不會顯示此規則，而是將它指派給變數 $a。此範例的第二行會將字串 "Outbound Rule 1" 指派給變數 $a 的 Name 屬性，此變數包含對於規則 site:Redmond/OBR1 的參照。在此範例的最後一行，我們呼叫 **Set-CsOutboundTranslationRule** Cmdlet、指定 Instance 參數，然後將之傳送給變數 $a。如果我們現在呼叫 **Get-CsOutboundTranslationRule** Cmdlet 並將 Identity 值指定為 site:Redmond/OBR1，則不會傳回任何項目。這是因為具有該 Identity 的規則已不存在，它已由 Identity 為 site:Redmond/Outbound Rule 1 的相同規則所取代。

    $a = Get-CsOutboundTranslationRule -Identity "site:Redmond/OBR1"
    $a.Name = "Outbound Rule 1"
    Set-CsOutboundTranslationRule -Instance $a

## 詳細描述

Lync Server 會將電話號碼正規化成 E.164 格式。但是，有許多專用交換機 (PBX) 系統無法使用這個格式。將號碼傳送到 中繼伺服器 或閘道之前，外撥轉譯規則會將號碼轉譯為區域撥號格式。呼叫此 Cmdlet 來修改現有的外撥轉譯規則。

每個外撥轉譯規則會與主幹組態相關聯。這表示使用此 Cmdlet 來修改規則，將影響對應的主幹組態。每個組態都可以與多個外撥轉譯規則相關聯。因此，每個規則的 Identity 是由一個範圍以及此範圍內的唯一名稱 (格式為「範圍/名稱」，例如 site:Redmond/OBR1) 所組成。規則會自動與相同範圍的主幹組態產生關聯。建議您呼叫 **Set-CsOutboundTranslationRule** Cmdlet 來變更主幹組態的外撥轉譯規則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsOutboundTranslationRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsOutboundTranslationRule"}

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>易瞭解外撥轉譯規則的描述。此描述可用來協助系統管理員清楚識別規則的目的。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsIdentity</p></td>
<td><p>您要修改之外撥轉譯規則的唯一識別碼。Identity 是由範圍後面加上在每個範圍內的唯一名稱所組成。例如，Redmond/OutboundRule1。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>TranslationRule</p></td>
<td><p>外撥轉譯規則的物件參照。此物件的類型必須是 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule，呼叫 <strong>Get-CsOutboundTranslationRule</strong> Cmdlet 即可擷取此物件。</p></td>
</tr>
<tr class="even">
<td><p><em>Pattern</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>規則運算式，表示 Translation 將套用的號碼模式。</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>如果號碼符合多個外撥轉譯規則的 Pattern，將根據優先順序套用規則。使用此參數指定規則的優先順序。</p></td>
</tr>
<tr class="even">
<td><p><em>Translation</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>規則運算式，將套用至符合 Pattern 的號碼，使號碼準備好以便輸出路由。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule 物件。接受外撥轉譯規則物件的管線傳送資料。

## 傳回類型

此 Cmdlet 不會傳回值，而會修改 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule 類型的物件。

## 請參閱

#### 其他資源

[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Remove-CsOutboundTranslationRule](remove-csoutboundtranslationrule.md)  
[Get-CsOutboundTranslationRule](get-csoutboundtranslationrule.md)

