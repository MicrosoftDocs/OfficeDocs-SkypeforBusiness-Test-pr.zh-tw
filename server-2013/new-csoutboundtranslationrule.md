---
title: New-CsOutboundTranslationRule
TOCTitle: New-CsOutboundTranslationRule
ms:assetid: aa6011e5-c48d-4fcc-ba65-bdec341234ed
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412803(v=OCS.15)
ms:contentKeyID: 49291974
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsOutboundTranslationRule

 

_**上次修改主題的時間：** 2015-03-09_

建立新的外撥轉譯規則。外撥轉譯規則會將電話號碼轉換成當地的撥號格式，以與專用交換機 (PBX) 系統互動。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsOutboundTranslationRule -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsOutboundTranslationRule -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

這個範例會為 Redmond 網站建立新的外撥轉譯規則，名為 Prefix Redmond。由於未指定其他參數，因此會使用預設值建立規則。請注意，傳遞至 Identity 參數的值會以雙引號括住；這是因為規則的名稱 (Prefix Redmond) 包含空格。如果規則名稱不含空格，則不必以雙引號括住 Identity。

    New-CsOutboundTranslationRule -Identity "site:Redmond/Prefix Redmond"

## 範例 2

這個範例會建立新的全域外撥轉譯規則，名為 SeattleSevenDigit (注意：我們可以不指定 Parent 和 Name，改為指定 -Identity global/SeattleSevenDigit 以建立相同的規則)。我們加入了 Description，說明這個規則用於將 E.164 格式的號碼轉譯為七位數字格式。此外也指定了 Pattern 和 Translation 值。這些值會將利用規則運算式以 Pattern 指定的 E.164 號碼 (在此範例中是以 +1425 開頭的 12 位數字) 移去前面 5 個數字，轉譯為 7 位數字。例如，號碼 +14255551212 將轉譯為號碼 5551212。

    New-CsOutboundTranslationRule -Parent global -Name SeattleSevenDigit -Description "Convert to seven digits" -Pattern '^\+1425(\d{7})$' -Translation '$1'

## 詳細描述

呼叫此 Cmdlet 可以建立新的外撥轉譯規則。Lync Server 會將電話號碼正規化成 E.164 格式。但是，有許多專用交換機 (PBX) 系統無法使用這個格式。將號碼傳送到中繼伺服器或閘道之前，外撥轉譯規則會將號碼轉譯為區域撥號格式。

每個外撥轉譯規則會與主幹組態相關聯。每個組態都可以與多個外撥轉譯規則相關聯。因此，每個規則的 Identity 是由一個範圍以及此範圍內的唯一名稱 (格式為「範圍/名稱」，例如 site:Redmond/OBR1) 所組成。規則會自動與相同範圍的主幹組態產生關聯。如果您呼叫 **New-CsOutboundTranslationRule** Cmdlet 並指定尚未定義主幹組態的範圍，就會利用指定的範圍、外撥轉譯規則及預設值來建立主幹組態。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsOutboundTranslationRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsOutboundTranslationRule"}

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
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>外撥轉譯規則的唯一識別碼。Identity 包括已套用規則的範圍和規則名稱，必須是在全域、網站或服務 (僅限 PSTNGateway) 範圍內。例如，site:Redmond/OutboundRule1 和 PstnGateway:Redmond.litwareinc.com/OutboundRule2。</p>
<p>如果指定了 Identity 參數，則不能指定 Name 或 Parent 參數的值。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>外撥轉譯規則的名稱。如果沒有提供 Name，就必須指定包含範圍和名稱的 Identity。如果提供 Name，也需要提供 Parent 參數，但不可指定 Identity。</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>外撥轉譯規則的範圍。如指定此參數的值，也必須指定 Name 參數的值。但是，不可指定 Identity 參數。如果沒有指定 Parent 和 Name 參數，則必須指定 Identity。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>外撥轉譯規則的描述。此描述將有助於瞭解規則的用途。</p></td>
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
<td><p><em>Pattern</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>規則運算式，表示 Translation 將套用的號碼模式。</p>
<p>預設值：^\+(\d*)$</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>如果號碼符合多個外撥轉譯規則的 Pattern，將根據優先順序套用規則。使用此參數指定規則的優先順序。</p></td>
</tr>
<tr class="even">
<td><p><em>Translation</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>規則運算式，將套用至符合 Pattern 的號碼，使號碼準備好以便輸出路由。</p>
<p>預設值：$1</p></td>
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

此 Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsOutboundTranslationRule](remove-csoutboundtranslationrule.md)  
[Set-CsOutboundTranslationRule](set-csoutboundtranslationrule.md)  
[Get-CsOutboundTranslationRule](get-csoutboundtranslationrule.md)

