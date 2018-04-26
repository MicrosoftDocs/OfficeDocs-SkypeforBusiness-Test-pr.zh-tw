---
title: New-CsVoiceTestConfiguration
TOCTitle: New-CsVoiceTestConfiguration
ms:assetid: da312c27-bc89-46c3-a6c9-c098ed4e7df7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398961(v=OCS.15)
ms:contentKeyID: 49292498
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoiceTestConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立用以測試電話號碼是否符合指定路由與規則的測試案例。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsVoiceTestConfiguration -Name <String> <COMMON PARAMETERS>

    New-CsVoiceTestConfiguration -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DialedNumber <String>] [-ExpectedRoute <String>] [-ExpectedTranslatedNumber <String>] [-ExpectedUsage <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-TargetDialplan <String>] [-TargetVoicePolicy <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

這個範例會以預設值建立 Identity 為 TestConfig1 的新語音測試設定。

    New-CsVoiceTestConfiguration -Identity TestConfig1

## 範例 2

這個範例會建立名為 TestConfig1 的新語音測試設定，並將 TargetDialplan 參數設定為 site:Redmond1。這會產生預計針對網站 Redmond1 的撥號對應表設定執行的號碼、使用方式和路由的測試。

我們在這個範例中宣告 TestConfig1，但不指定 Identity 參數。由於 Identity 是位置參數，因此 Cmdlet 會將命令中的 Cmdlet 名稱後的第一個值辨識為 Identity。

    New-CsVoiceTestConfiguration TestConfig1 -TargetDialplan site:Redmond1

## 範例 3

這個範例會建立名為 TestConfig1 的新語音測試設定。這個設定會使用預設值測試 DialedNumber 5551212，預計的輸出 (ExpectedTranslatedNumber) 為 +5551212。此預期根據將在針對這個物件執行測試時使用的撥號對應表關聯的正規化規則為基礎。必須使用 **Test-CsVoiceTestConfiguration** Cmdlet 執行該測試。

    New-CsVoiceTestConfiguration -Identity TestConfig1 -DialedNumber 5551212 -ExpectedTranslatedNumber +5551212

## 詳細描述

在實作語音路由和語音原則之前，最好先以不同的電話號碼來測試，以確保結果符合您的預期。可以使用這個 Cmdlet 建立測試案例以執行此測試。

**New-CsVoiceTestConfiguration** Cmdlet 會定義語音路由、使用方式、撥號對應表和據以測試指定之電話號碼的語音原則。此資訊的所有相關資訊都可使用其他 Cmdlet 來定義和擷取；請參閱本主題的參數描述，以取得詳細資訊。

使用此 Cmdlet 所建立的設定可透過 **Test-CsVoiceTestConfiguration** Cmdlet 來測試。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsVoiceTestConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoiceTestConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>唯一識別此一測試案例的字串。</p>
<p>這個字串最多可以有 32 個字元，並可包含任何英數字元，加上反斜線 (\)、句點 (.) 或底線 (_)。</p>
<p>此參數的值不含範圍，因為此物件只能在全域範圍上建立。因此，只需要唯一名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此參數所含的值與 Identity 相同。如有指定 Identity 參數，即不可在命令中加入 Name 參數。同樣地，如有指定 Name 參數，亦不可指定 Identity。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DialedNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>您要用來測試原則、使用方式等的電話號碼。</p>
<p>必須是 512 個或更少的字元。</p>
<p>預設值：1234</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedRoute</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>預期在設定測試期間使用的語音路由名稱。如果使用不同的路由，根據目標撥號對應表和語音原則，測試將會失敗。您可以呼叫 <strong>Get-CsVoiceRoute</strong> Cmdlet 來擷取可用的語音路由。</p>
<p>必須是 256 個或更少的字元。</p></td>
</tr>
<tr class="even">
<td><p><em>ExpectedTranslatedNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>以您預期在轉換之後的格式所呈現的電話號碼。這是在正規化後 DialedNumber 參數的值。如果您執行 <strong>Test-CsVoiceTestConfiguration</strong> Cmdlet，而 DialedNumber 並未產生 ExpectedTranslatedNumber 中的值，則測試會報告為 Fail。</p>
<p>必須是 512 個或更少的字元。</p>
<p>預設值：+1234</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedUsage</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>預期在組態測試期間使用的 PSTN 使用方式的名稱。如果根據目標撥號對應表和語音原則而使用不同的 PSTN 使用方式，則測試將會失敗。您可以呼叫 <strong>Get-CsPstnUsage</strong> Cmdlet 來擷取可用的使用方式。</p>
<p>必須是 256 個或更少的字元。</p></td>
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
<td><p><em>TargetDialplan</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要用於此測試之撥號對應表的 Identity。您可以呼叫 <strong>Get-CsDialPlan</strong> Cmdlet 來擷取撥號對應表。</p>
<p>必須是 40 個或更少的字元。</p>
<p>預設值：全球</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetVoicePolicy</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>執行此測試所針對之語音原則的 Identity。您可以呼叫 <strong>Get-CsVoicePolicy</strong> Cmdlet 來擷取語音原則。</p>
<p>必須是 40 個或更少的字元。</p>
<p>預設值：全球</p></td>
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

此 Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration 類型的物件

## 請參閱

#### 其他資源

[Remove-CsVoiceTestConfiguration](remove-csvoicetestconfiguration.md)  
[Set-CsVoiceTestConfiguration](set-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)  
[Test-CsVoiceTestConfiguration](test-csvoicetestconfiguration.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)

