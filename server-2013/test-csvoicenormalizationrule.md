---
title: Test-CsVoiceNormalizationRule
TOCTitle: Test-CsVoiceNormalizationRule
ms:assetid: e2d27ce1-883f-4679-a288-f35846842258
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399003(v=OCS.15)
ms:contentKeyID: 49292602
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsVoiceNormalizationRule

 

_**上次修改主題的時間：** 2015-03-09_

測試電話號碼是否符合語音正規化規則，並在套用正規化規則之後傳回該號碼。語音正規化規則可用於將電話撥號要求 (例如撥打外線之前先撥 9) 轉換成 Lync Server 所使用的 E.164 電話號碼格式。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsVoiceNormalizationRule -DialedNumber <PhoneNumber> -NormalizationRule <NormalizationRule>

## 範例

## 範例 1

這個範例會對 Identity 為 "global/11 digit number rule" 的語音正規化規則執行語音正規化測試。首先會執行 **Get-CsVoiceNormalizationRule** Cmdlet 以擷取 Identity 為 "global/11 digit number rule" 的規則。接著將該規則物件傳送至 **Test-CsVoiceNormalizationRule** Cmdlet，在此會針對電話號碼 14255559999 測試該規則。在套用語音正規化規則 "global/11 digit number rule" 之後，輸出將會是 DialedNumber。如果這個規則並未套用至 DialedNumber 值 (例如，如果正規化規則符合 11 位數號碼的模式，而您提供 7 位數的號碼)，則不會傳回任何值。

    Get-CsVoiceNormalizationRule -Identity "global/11 digit number rule" | Test-CsVoiceNormalizationRule -DialedNumber 14255559999

## 範例 2

範例 2 與範例 1 相同，只是它不會直接將 Get 作業的結果傳送至 Test Cmdlet，而是會先將物件儲存在變數 $a 中，然後以值的形式傳遞到 NormalizationRule 參數，當作對其執行測試的語音正規化規則來使用。

    $a = Get-CsVoiceNormalizationRule -Identity "global/11 digit number rule"
    Test-CsVoiceNormalizationRule -DialedNumber 5551212 -NormalizationRule $a

## 範例 3

這個範例會對定義於 Lync Server 部署中的所有語音正規化規則執行語音正規化測試。首先會執行 **Get-CsVoiceNormalizationRule** Cmdlet (不含參數)，以擷取所有語音正規化規則。傳回的規則集合接著便會傳送至 **Test-CsVoiceNormalizationRule** Cmdlet，其中集合中的每個規則都會針對電話號碼 2065559999 進行測試。輸出將會是轉譯號碼清單，且每個測試過的規則皆有一份清單。如果規則並未套用至 DialedNumber 值 (例如，若正規化規則符合 11 位數號碼的模式，而您提供 7 位數的號碼)，清單中將會針對該規則出現空白行。

    Get-CsVoiceNormalizationRule | Test-CsVoiceNormalizationRule -DialedNumber 2065559999

## 詳細描述

這個 Cmdlet 可讓您查看將語音正規化規則套用到特定電話號碼後的結果。語音正規化規則是電話授權和電話轉接的必要部分。這些規則定義將號碼從通常由使用者輸入的格式轉換 (或轉譯) 為標準 (E.164) 格式的需求。請使用此 Cmdlet 來疑難排解撥號問題，或確認該規則會根據指定的號碼如預期運作。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsVoiceNormalizationRule** Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsVoiceNormalizationRule"}

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
<td><p>Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
<td><p>您想要用來測試正規化規則的電話號碼，會在 NormalizationRule 參數中指定。</p>
<p>完整資料類型：Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
</tr>
<tr class="even">
<td><p><em>NormalizationRule</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule</p></td>
<td><p>包含正規化規則參照的物件，您想要用此撥號對應表來測試 DialedNumber 參數中所指定的號碼。</p>
<p>您可以呼叫 <strong>Get-CsVoiceNormalizationRule</strong> Cmdlet 來擷取語音正規化規則。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule 物件。接受管線傳送的語音正規化規則物件輸入。

## 傳回類型

傳回 Microsoft.Rtc.Management.Voice.NormalizationRuleTestResult 類型的物件。

## 請參閱

#### 其他資源

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)

