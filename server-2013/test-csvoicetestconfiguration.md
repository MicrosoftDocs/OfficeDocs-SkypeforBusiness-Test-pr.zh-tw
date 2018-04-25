---
title: Test-CsVoiceTestConfiguration
TOCTitle: Test-CsVoiceTestConfiguration
ms:assetid: 1c87ef27-0542-49b0-9125-512fd6ed187d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398260(v=OCS.15)
ms:contentKeyID: 49290270
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsVoiceTestConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

執行語音設定測試，以確保語音路由和原則如預期運作。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsVoiceTestConfiguration -TestCaseInputObject <TestConfiguration> [-Dialplan <LocationProfile>] [-RouteSettings <PstnRoutingSettings>] [-VoicePolicy <VoicePolicy>] <COMMON PARAMETERS>

    Test-CsVoiceTestConfiguration -DialedNumber <String> -Dialplan <LocationProfile> -VoicePolicy <VoicePolicy> [-RouteSettings <PstnRoutingSettings>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>]

## 範例

## 範例 1

此範例會針對設定 TestConfig1 來執行語音設定測試。首先執行 **Get-CsVoiceTestConfiguration** Cmdlet，以擷取 Identity 為 TestConfig1 的設定。然後，將該設定物件傳送給 **Test-CsVoiceTestConfiguration** Cmdlet。

    Get-CsVoiceTestConfiguration -Identity TestConfig1 | Test-CsVoiceTestConfiguration

## 範例 2

範例 2 與範例 1 相同，只除了它不是直接將 Get 作業的結果傳送至 Test Cmdlet，而是物件會先儲存在變數 $a 中，然後以值的形式傳遞到 TestCaseInputObject 參數，用作測試設定。

    $a = Get-CsVoiceTestConfiguration -Identity TestConfig1
    Test-CsVoiceTestConfiguration -TestCaseInputObject $a

## 範例 3

此範例會執行測試設定，但不事先以 **New-CsVoiceTestConfiguration** Cmdlet 定義。此範例不會傳遞事先建立的 TestConfiguration 物件，而是示範如何藉由指定要測試的撥打號碼，以及透過執行測試所根據的撥號對應表和語音原則，以「即時」設定測試。

此範例的第一行會呼叫 **Get-CsDialPlan** Cmdlet 以擷取 Global 撥號對應表。擷取的撥號對應表物件會指派給 $dp 變數。在第二行，呼叫 **Get-CsVoicePolicy** Cmdlet 以擷取 Global 語音原則，然後將該原則指派給 $vp 變數，即可以相同的方式來處理語音原則。

最後，便可準備執行測試。我們呼叫 **Test-CsVoiceTestConfiguration** Cmdlet，將要測試的電話號碼傳遞至 DialedNumber 參數、將第 1 行中擷取的撥號對應表 (儲存在 $dp 中) 傳遞至 Dialplan 參數，然後將第 2 行中擷取的語音原則 (儲存在 $vp 中) 傳遞至 VoicePolicy 參數。

請注意，範例 3 的輸出不含預期結果的狀態。如果您想要對照期望來測試結果，必須使用 **New-CsVoiceTestConfiguration** Cmdlet 並呼叫 **Test-CsVoiceTestConfiguration** Cmdlet 來定義這些期望，如範例 1 和 2 所示。

    $dp = Get-CsDialPlan -Identity Global
    $vp = Get-CsVoicePolicy -Identity Global
    Test-CsVoiceTestConfiguration -DialedNumber 4255551212 -Dialplan $dp -VoicePolicy $vp

## 詳細描述

在實作語音路由和語音原則之前，最好先以不同的電話號碼來測試，以確保結果符合您的預期。使用適當的參數設定來執行此 Cmdlet 可讓您執行這些測試。

此 Cmdlet 會根據語音路由、使用方式、撥號對應表和語音原則來測試電話號碼，可讓您驗證期望結果，或比較實際結果與預期結果。您可以個別地輸入適當參數，或使用 **New-CsVoiceTestConfiguration** Cmdlet，以定義要測試的語音組態。

如果您輸入 DialedNumber、DialPlan 和 VoicePolicy 的值，輸出會包含轉譯的號碼、用來建立該轉譯的正規化規則、使用的路由及 PSTN 用途。如果您輸入 TestCaseInputObject 參數的值，則您也可以擷取狀態，以瞭解結果是否符合您以 **New-CsVoiceTestConfiguration** Cmdlet 建立測試物件時所提供的預期結果。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsVoiceTestConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsVoiceTestConfiguration"}

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
<td><p><em>DialedNumber</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>執行測試的電話號碼。根據撥號對應表、路由和原則，此號碼會經過正規化並顯示為輸出。</p>
<p>除非提供 TestCaseInputObject 參數的值，否則需要此參數。您不能提供 DialedNumber 和 TestCaseInputObject(TestCaseInputObject 在該物件內已包含 DialedNumber)。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Dialplan</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile</p></td>
<td><p>執行測試時，針對要使用之撥號對應表的撥號對應表物件的參照。您可以呼叫 <strong>Get-CsDialPlan</strong> Cmdlet 來擷取撥號對應表物件。</p>
<p>如果您也已指定 DialedNumber 參數，則需要此參數。如果您使用 TestCaseInputObject 參數，請不要使用此參數。如果使用的話，此參數中的物件必須符合 TestCaseInputObject 中指定的撥號對應表，因此使用此參數變得多餘。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>TestCaseInputObject</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration</p></td>
<td><p>物件，含有要測試之語音設定的參照。您可以呼叫 <strong>Get-CsVoiceTestConfiguration</strong> Cmdlet 來擷取此物件參照。</p>
<p>如果您使用此參數呼叫 Cmdlet，即不可指定 DialedNumber。您也不應該指定 Dialplan 或 VoicePolicy，因為這些參數會與語音測試設定物件中的值重複。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>VoicePolicy</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy</p></td>
<td><p>在執行測試時，要使用之語音原則的語音原則物件的參照。您可以呼叫 <strong>Get-CsVoicePolicy</strong> Cmdlet 來擷取語音原則物件。</p>
<p>如果您也已指定 DialedNumber 參數，則需要此參數。如果您使用 TestCaseInputObject 參數，請不要使用此參數。如果使用的話，此參數中的物件必須符合 TestCaseInputObject 中指定的語音原則，因此使用此參數變得多餘。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>RouteSettings</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnRoutingSettings</p></td>
<td><p>物件的參照，含有 Lync Server 安裝上所有可用的語音路由。您可以呼叫 <strong>Get-CsRoutingConfiguration</strong> Cmdlet 來擷取此物件。</p>
<p>您可以搭配 DialedNumber 參數或 TestCaseInputObject 參數來使用此參數。</p>
<p></p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration 物件。接受管線傳送的語音測試組態物件輸入。

## 傳回類型

此 Cmdlet 會傳回 Microsoft.Rtc.Management.Voice.OcsVoiceTestResult 類型的物件。

## 請參閱

#### 其他資源

[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Remove-CsVoiceTestConfiguration](remove-csvoicetestconfiguration.md)  
[Set-CsVoiceTestConfiguration](set-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Get-CsRoutingConfiguration](get-csroutingconfiguration.md)

