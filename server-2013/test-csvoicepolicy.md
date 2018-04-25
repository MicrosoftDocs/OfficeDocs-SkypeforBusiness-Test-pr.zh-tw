---
title: Test-CsVoicePolicy
TOCTitle: Test-CsVoicePolicy
ms:assetid: 4d631e36-3a9d-4ca2-913f-8c9f4e93183d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398310(v=OCS.15)
ms:contentKeyID: 49290865
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsVoicePolicy

 

_**上次修改主題的時間：** 2015-03-09_

測試電話號碼是否符合語音原則，並根據原則為該號碼指定所要使用的路由。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsVoicePolicy -TargetNumber <PhoneNumber> -VoicePolicy <VoicePolicy> [-Force <SwitchParameter>] [-RouteSettings <PstnRoutingSettings>]

## 範例

## 範例 1

此範例會針對 Identity 為 site:Redmond 的語音原則執行語音原則測試。首先會執行 **Get-CsVoicePolicy** Cmdlet 擷取 Identity 為 site:Redmond 的原則。接著，該原則物件會傳送到 **Test-CsVoicePolicy** Cmdlet，以電話號碼 +14255559999 來測試該原則。其輸出將會是具有符合 TargetNumber 值之電話模式，並具有符合原則中電話使用方式之電話使用方式的第一個語音路由 (根據路由的 Priority 屬性)。如果找不到符合的路由 (例如，如果號碼模式符合 11 位數模式，而您提供的是 7 位數號碼)，則會傳回 Null 值。

    Get-CsVoicePolicy -Identity site:Redmond | Test-CsVoicePolicy -TargetNumber "+14255559999"

## 範例 2

範例 2 與範例 1 相同，只除了它不是直接將 Get 作業的結果傳送至 **Test-CsVoicePolicy** Cmdlet，而是物件會先以變數 $a 儲存，然後以值的形式傳遞到 VoicePolicy 參數，用來做為執行測試所依據的原則。

    $a = Get-CsVoicePolicy -Identity site:Redmond
    Test-CsVoicePolicy -TargetNumber "+14255559999" -VoicePolicy $a

## 範例 3

此範例會針對 Lync Server 部署中定義的所有語音原則執行語音原則測試。首先會執行 **Get-CsVoicePolicy** Cmdlet (不含任何參數) 以擷取所有語音原則。然後，傳回的原則集合會傳送到 **Test-CsVoicePolicy** Cmdlet，根據所提供的目標電話號碼 (+12065559999) 及電話使用方式，檢查集合中每個原則的符合路由。其輸出將會是符合路由的清單，加上符合的電話使用方式。

    Get-CsVoicePolicy | Test-CsVoicePolicy -TargetNumber "+12065559999"

## 詳細描述

語音原則透過公用交換電話網路 (PSTN) 使用方式而與語音路由產生關聯。已被指派特定語音原則之使用者所撥打的電話，只能透過具有符合該原則之使用方式的 PSTN 使用方式的路由，以及符合所撥出號碼的號碼模式來傳送。呼叫 **Test-CsVoicePolicy** Cmdlet 來判斷哪一個路由 (如果有的話) 會用來路由傳送擁有特定語音原則之使用者的來電，並判斷將原則繫結至路由的電話使用方式。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsVoicePolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsVoicePolicy"}

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
<td><p><em>TargetNumber</em></p></td>
<td><p>必要</p></td>
<td><p>PhoneNumber</p></td>
<td><p>據以執行測試的電話號碼。此號碼應該採用 E.164 格式 (例如 +14255551212)。</p></td>
</tr>
<tr class="even">
<td><p><em>VoicePolicy</em></p></td>
<td><p>必要</p></td>
<td><p>VoicePolicy</p></td>
<td><p>要針對其執行測試之語音原則物件的參考。您可以呼叫 <strong>Get-CsVoicePolicy</strong> Cmdlet 來擷取語音原則物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏當執行 Cmdlet 時可能發生的任何確認提示或非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>RouteSettings</em></p></td>
<td><p>選用</p></td>
<td><p>PstnRoutingSettings</p></td>
<td><p>據以執行測試的路由設定。您可以透過呼叫 <strong>Get-CsRoutingConfiguration</strong> Cmdlet 來擷取路由設定。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy 物件。接受管線傳送的語音原則物件輸入。

## 傳回類型

傳回 Microsoft.Rtc.Management.Voice.VoicePolicyTestResult 類型的物件。

## 請參閱

#### 其他資源

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)

