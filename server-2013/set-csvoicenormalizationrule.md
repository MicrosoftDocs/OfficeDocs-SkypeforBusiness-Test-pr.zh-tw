---
title: Set-CsVoiceNormalizationRule
TOCTitle: Set-CsVoiceNormalizationRule
ms:assetid: 68850abb-4ac7-4ae1-bb6e-d991385f92a4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398491(v=OCS.15)
ms:contentKeyID: 49291185
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceNormalizationRule

 

_**上次修改主題的時間：** 2015-03-09_

修改語音正規化規則。語音正規化規則可用於將電話撥號要求 (例如撥打外線之前先撥 9) 轉換成 Lync Server 所使用的 E.164 電話號碼格式。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsVoiceNormalizationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceNormalizationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-IsInternalExtension <$true | $false>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

這個範例將網站 Redmond 上 Prefix Redmond 規則的描述設定為 "Add a prefix to all numbers on site Redmond"。

    Set-CsVoiceNormalizationRule -Identity "site:Redmond/Prefix Redmond" -Description "Add a prefix to all numbers on site Redmond"

## 範例 2

這個範例會修改 Identity 為 global/SeattleFourDigit 的語音正規化規則。其會指定新的 Description 以反映規則修改。此外，也已指定 Translation 值，此值會修改規則以將符合此規則現有模式的任何號碼轉譯為相同的號碼，但是加上首碼 +1206556。例如，如果現有的模式符合任何四位數的號碼並輸入數字 1234，此規會將該分機轉譯為號碼 +12065561234。

    Set-CsVoiceNormalizationRule -Identity global/SeattleFourDigit -Description "Translate an internal four-digit extension" -Translation '+1206556$1'

## 範例 3

範例 3 會變更正規化規則的名稱。請記住，變更名稱也會變更 Identity 的名稱部分。**Set-CsVoiceNormalizationRule** Cmdlet 沒有 Name 參數，因此為了變更名稱，我們會先呼叫 **Get-CsVoiceNormalizationRule** Cmdlet 以擷取 Identity 為 global/RedmondFourDigit 的規則，並將傳回的物件指定給變數 $a。然後將字串 RedmondRule 指定給物件的 Name 屬性。接著將變數傳遞給 **Set-CsVoiceNormalizationRule** Cmdlet 的 Instance 參數，讓變更生效。

    $a = Get-CsVoiceNormalizationRule -Identity global/RedmondFourDigit
    $a.name = "RedmondRule"
    Set-CsVoiceNormalizationRule -Instance $a

## 詳細描述

此 Cmdlet 會修改具名的語音正規化規則。這些規則是電話授權和電話路由的必要部分。它們定義將號碼從內部 Lync Server 格式轉換 (或轉譯) 為標準 (E.164) 格式的需求。了解規則運算式對於定義將要轉譯的號碼模式很有幫助。

使用這個 Cmdlet 修改的規則屬於撥號對應表，而且除了使用 **Get-CsVoiceNormalizationRule** Cmdlet 存取之外，也可以使用對 **Get-CsDialPlan** Cmdlet 的呼叫所傳回的 NormalizationRules 屬性存取。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsVoiceNormalizationRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceNormalizationRule"}

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
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>正規化規則的簡易描述。</p>
<p>字串長度上限：512 個字元。</p></td>
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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>規則的唯一識別碼。指定的 Identity 必須包含範圍，後面接正斜線和名稱，例如：site:Redmond/Rule1，其中 site:Redmond 是範圍，Rule1 是名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>NormalizationRule</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。 此物件的類型必須是 NormalizationRule，並可由呼叫 <strong>Get-CsVoiceNormalizationRule</strong> Cmdlet 擷取此物件。</p></td>
</tr>
<tr class="even">
<td><p><em>IsInternalExtension</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，套用此規則的結果會是企業內部的號碼。若為 False，套用規則會產生外部號碼。如果相關撥號對應表之 OptimizeDeviceDialing 內容的值已設為 False，這個值便會被忽略。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Pattern</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>一個規則運算式，撥打的號碼必須與其相符，才會套用此規則。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>套用規則的順序。一個號碼可能符合多個規則。此參數會設定針對號碼測試規則的順序。</p></td>
</tr>
<tr class="odd">
<td><p><em>Translation</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要套用至號碼的規則運算式模式，以將號碼轉換為 E.164 格式。</p>
<p></p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule 物件。**Set-CsVoiceNormalizationRule** Cmdlet 接受管線傳送的語音正規化規則物件輸入。

## 傳回類型

**Set-CsVoiceNormalizationRule** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)

