---
title: New-CsVoiceNormalizationRule
TOCTitle: New-CsVoiceNormalizationRule
ms:assetid: 189809ff-559e-476a-a32c-8b3812371883
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398240(v=OCS.15)
ms:contentKeyID: 49290228
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoiceNormalizationRule

 

_**上次修改主題的時間：** 2015-03-09_

建立新的語音正規化規則。語音正規化規則可用於將電話撥號要求 (例如撥打外線之前先撥 9) 轉換成 Lync Server 所使用的 E.164 電話號碼格式。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsVoiceNormalizationRule -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsVoiceNormalizationRule -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-IsInternalExtension <$true | $false>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

這個範例會為 Redmond 網站建立名為 Prefix Redmond 的新語音正規化規則。由於未指定其他參數，因此會使用預設值建立規則。請注意，傳遞至 Identity 參數的值會以雙引號括住；這是因為規則的名稱 (Prefix Redmond) 包含空格。如果規則名稱不含空格，則不必以雙引號括住 Identity。

請記住，Redmond 網站的撥號對應表必須存在，此命令才會成功。您可以呼叫 **New-CsDialPlan** Cmdlet，建立新撥號對應表。

    New-CsVoiceNormalizationRule -Identity "site:Redmond/Prefix Redmond"

## 範例 2

此範例會建立名為 SeattleFourDigit 的新語音正規化規則，套用至含有 Identity SeattleUser 的每個使用者撥號對應表(注意：我們可以不指定 Parent 和 Name，改為指定 -Identity SeattleUser/SeattleFourDigit 以建立相同的規則)。我們包含了 Description，說明這個規則用於轉譯由只有 4 位數分機在內部撥打的號碼。此外也指定了 Pattern 和 Translation 值。這些值將四位數的號碼 (由 Pattern 中的規則運算式指定) 轉換為相同的四位數號碼，但是前面會加上 Translation 值 (+1206555)。例如，如果輸入分機 1234，這個規則會將分機轉譯為號碼 +12065551234。

請注意 Pattern 和 Translation 值周圍的單引號。這些值必須要有單引號；雙引號 (或沒有任何引號) 將無法使這些值在這個情況下發揮作用。

如同範例 1，含有給定範圍的撥號對應表必須存在。在這種情況下，這表示 Identity 為 SeattleUser 的撥號對應表必須已經存在。

    New-CsVoiceNormalizationRule -Parent SeattleUser -Name SeattleFourDigit -Description "Dialing with internal four-digit extension" -Pattern '^(\d{4})$' -Translation '+1206555$1'

## 詳細描述

此 Cmdlet 會建立具名的語音正規化規則。這些規則是電話授權和電話路由的必要部分。它們定義將號碼從內部 Lync Server 格式轉換 (或轉譯) 為標準 (E.164) 格式的需求。了解規則運算式對於定義將要轉譯的號碼模式很有幫助。

使用這個 Cmdlet 建立的規則屬於撥號對應表，而且除了使用 **Get-CsVoiceNormalizationRule** Cmdlet 存取之外，也可以使用對 **Get-CsDialPlan** Cmdlet 的呼叫所傳回的 NormalizationRules 屬性存取。除非符合正規化規則 Identity 中指定範圍的含有 Identity 的撥號對應表已經存在，否則無法建立正規化規則。例如，除非 site:Redmond 的撥號對應表已經存在，否則無法使用 Identity site:Redmond/RedmondNormalizationRule 建立正規化規則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsVoiceNormalizationRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoiceNormalizationRule"}

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
<td><p>規則的唯一識別碼。指定的 Identity 必須包含範圍，後面接正斜線和名稱，例如：site:Redmond/Rule1，其中 site:Redmond 是範圍，Rule1 是名稱。名稱部分會自動儲存在 Name 屬性中。您無法在同一個命令中指定 Identity 和 Name 的值。</p>
<p>語音正規化規則可在下列範圍內建立：全域、網站、服務 (僅限登錄器和 PSTN 閘道)、個別使用者。Identity 和語音正規化規則之範圍相符的撥號對應表必須已存在，如此才能建立新規則 (若要擷取撥號對應表的清單，請呼叫 <strong>Get-CsDialPlan</strong> Cmdlet)。</p>
<p>除非指定了 Parent 參數，否則需要 Identity 參數。同一個命令中不能同時包含 Identity 參數和 Parent 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>規則的名稱。如果指定了 Parent 參數的值，必須使用此參數。若未指定 Parent 參數的值，Name 會預設為 Identity 參數中指定的名稱。例如，如果以 Identity site:Redmond/RedmondRule 建立規則，Name 預設為 RedmondRule。不能在同一個命令中同時使用 Name 參數和 Identity 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>將要建立新正規化規則的範圍。這個值必須為全域；site:&lt;網站名稱&gt;，其中 &lt;網站名稱&gt; 是 Lync Server 網站、PSTN 閘道或登錄器服務的名稱 (如 PSTNGateway:redmond.litwareinc.com)，或指定每個使用者規則的字串。含有指定範圍的撥號對應表必須已經存在，否則命令會失敗。</p>
<p>除非指定了 Identity 參數，否則需要 Parent 參數。同一個命令中不能同時包含 Identity 參數和 Parent 參數。如果包含 Parent 參數，也需要 Name 參數。</p></td>
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
<td><p>正規化規則的簡易描述。</p>
<p>字串長度上限：512 個字元。</p></td>
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
<td><p><em>IsInternalExtension</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，套用此規則的結果會是組織內部的號碼。若為 False，套用規則會產生外部號碼。如果相關撥號對應表之 OptimizeDeviceDialing 內容的值已設為 False，這個值便會被忽略。</p>
<p>預設值：False</p></td>
</tr>
<tr class="odd">
<td><p><em>Pattern</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>一個規則運算式，撥打的號碼必須與其相符，才會套用此規則。</p>
<p>預設值：^(\d{11})$ (預設代表任何數字集，最多 11 位數)。</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>套用規則的順序。一個電話號碼可能符合多個規則。此參數會設定針對號碼測試規則的順序。</p></td>
</tr>
<tr class="odd">
<td><p><em>Translation</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要套用至號碼的規則運算式模式，以將號碼轉換為 E.164 格式。</p>
<p>預設值：+$1 (預設會在號碼前面加上加號 [+])。</p></td>
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

無。

## 傳回類型

此 Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[New-CsDialPlan](new-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)

