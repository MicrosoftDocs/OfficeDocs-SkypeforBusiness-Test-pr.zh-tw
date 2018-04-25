---
title: Set-CsVoiceTestConfiguration
TOCTitle: Set-CsVoiceTestConfiguration
ms:assetid: 7b95fc95-ec0e-4bb3-aed1-e8b72e305999
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398614(v=OCS.15)
ms:contentKeyID: 49291419
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceTestConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改用以測試電話號碼是否符合指定路由與規則的測試案例。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsVoiceTestConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceTestConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DialedNumber <String>] [-ExpectedRoute <String>] [-ExpectedTranslatedNumber <String>] [-ExpectedUsage <String>] [-Force <SwitchParameter>] [-TargetDialplan <String>] [-TargetVoicePolicy <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例將 TestConfig1 的語音測試設定所撥打的號碼設為 14255551212。這是將根據語音原則和路由來檢查的號碼，目的是確定正規化如預期進行，以及確定套用的路由和撥號對應表都正確。

    Set-CsVoiceTestConfiguration -Identity TestConfig1 -DialedNumber 14255551212

## 範例 2

此範例修改語音測試設定 TestConfig1 的設定。此命令會將 TargetDialplan 設為 site:Redmond1 的撥號對應表。因為撥號對應表的變更可能意謂著正規化規則有所變更，所以 ExpectedTranslationNumber 也已變更，以反映該撥號對應表的正規化規則的預期結果。

    Set-CsVoiceTestConfiguration -Identity TestConfig1 -TargetDialplan site:Redmond1 -ExpectedTranslatedNumber "+912065551212"

## 詳細描述

在實作語音路由和語音原則之前，最好先以不同的電話號碼來測試，以確保結果符合您的預期。在作法上，您可以使用此 Cmdlet 來修改測試案例。

**Set-CsVoiceTestConfiguration** Cmdlet 會修改語音路由、使用方式、撥號對應表和據以測試指定之電話號碼的語音原則。本主題的參數描述中所指定的其他 Cmdlet，也都可以用來定義和擷取此資訊。

使用此 Cmdlet 所修改的設定可透過 **Test-CsVoiceTestConfiguration** Cmdlet 來測試。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsVoiceTestConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceTestConfiguration"}

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
<td><p><em>DialedNumber</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>您要用來測試原則、使用方式等的電話號碼。</p>
<p>必須為 512 個字元或更少。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedRoute</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>預期在設定測試期間使用的語音路由名稱。如果根據目標撥號對應表和語音原則使用不同的路由，則測試將會失敗。您可以呼叫 <strong>Get-CsVoiceRoute</strong> Cmdlet 來擷取可用的語音路由。</p>
<p>必須為 256 個字元或更少。</p></td>
</tr>
<tr class="even">
<td><p><em>ExpectedTranslatedNumber</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>以您預期在轉換之後的格式所呈現的電話號碼。這是在正規化後 DialedNumber 參數的值。如果您執行 <strong>Test-CsVoiceTestConfiguration</strong> Cmdlet，而 DialedNumber 並未產生 ExpectedTranslatedNumber 中的值，則測試會報告為 Fail。</p>
<p>必須為 512 個字元或更少。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedUsage</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>預期在組態測試期間使用的 PSTN 使用方式的名稱。如果根據目標撥號對應表和語音原則而使用不同的 PSTN 使用方式，則測試將會失敗。您可以呼叫 <strong>Get-CsPstnUsage</strong> Cmdlet 來擷取可用的使用方式。</p>
<p>必須為 256 個字元或更少。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>唯一識別您要修改之測試案例的字串。</p>
<p>此參數的值不含範圍，因為此物件只能在全域範圍上建立。因此只需要名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>TestConfiguration</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration 類型的物件，含現有的語音測試設定和您想對該設定進行的變更。此類型的物件可以透過呼叫 <strong>Get-CsVoiceTestConfiguraton</strong> Cmdlet 來擷取。</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetDialplan</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>要用於此測試之撥號對應表的 Identity。您可以呼叫 <strong>Get-CsDialPlan</strong> Cmdlet 來擷取撥號對應表。</p>
<p>必須為 40 個字元或更少。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetVoicePolicy</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>執行此測試所針對之語音原則的 Identity。您可以呼叫 <strong>Get-CsVoicePolicy</strong> Cmdlet 來擷取語音原則。</p>
<p>必須為 40 個字元或更少。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration 物件。接受管線傳送的語音測試組態物件輸入。

## 傳回類型

此 Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration 類型的物件。

## 請參閱

#### 其他資源

[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Remove-CsVoiceTestConfiguration](remove-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)  
[Test-CsVoiceTestConfiguration](test-csvoicetestconfiguration.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)

