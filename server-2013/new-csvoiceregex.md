---
title: New-CsVoiceRegex
TOCTitle: New-CsVoiceRegex
ms:assetid: a1a498b7-8353-40bd-9c02-424c95743ec3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412751(v=OCS.15)
ms:contentKeyID: 49291871
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoiceRegex

 

_**上次修改主題的時間：** 2015-03-09_

建立將電話號碼轉譯成其他格式的規則運算式模式與轉譯。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsVoiceRegex -AtLeastLength <Int32> [-DigitsToPrepend <String>] [-DigitsToStrip <Int32>] [-StartsWith <String>] <COMMON PARAMETERS>

    New-CsVoiceRegex -ExactLength <Int32> [-DigitsToPrepend <String>] [-DigitsToStrip <Int32>] [-StartsWith <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## 範例

## 範例 1

此範例會建立新的規則運算式模式與轉譯。此運算式包含一個必須確切為 7 個字元的模式 (-ExactLength 7)，而且會移除相符號碼的前三位數 (-DigitsToStrip 3)。此規則運算式建立的 Pattern 將為 ^\\d{3}(\\d{4})$，而 Translation 將為 $1。例如，號碼 5551212 會符合此模式，而結果產生的轉譯將為 1212，這是因為7 位數號碼已除去前 3 位數。

    $regex = New-CsVoiceRegex -ExactLength 7 -DigitsToStrip 3

## 範例 2

此範例也會建立新的規則運算式模式與轉譯，但是隨後會使用這些值來建立新的語音正規化規則。在第一行，我們呼叫 **New-CsVoiceRegEx** Cmdlet 來建立規則運算式，其中相符號碼必須至少有 7 個字元 (-AtLeastLength 7)，而且必須以 1 開頭 (-StartsWith "1")。此命令的結果會指派給變數 $regex。

在第二行，我們呼叫 **New-CsVoiceNormalizationRule** Cmdlet。我們賦與新規則唯一的名稱 (在此範例中為 global/internal rule)。然後，指派呼叫 **New-CsVoiceRegex** Cmdlet 後建立的 Pattern 做為正規化規則的 Pattern：-Pattern $regex.Pattern。我們也對 Translation 執行相同的動作，指派呼叫 **New-CsVoiceRegex** Cmdlet 後所建立的 Translation：-Translation $regex.Translation。

注意：在此範例中建立的模式為 ^(1\\d{5}\\d+)$。要解釋起來可以這樣說：號碼以 1 (1) 開頭、後接五個數字 (\\d{5})，再接任意位數 (\\d+)。這會形成至少 7 位數 (1 + 5 + 1 以上) 並以 1 開頭的號碼，也就是我們所要求的結果。

    $regex = New-CsVoiceRegex -AtLeastLength 7 -StartsWith "1"
    New-CsVoiceNormalizationRule "global/internal rule" -Pattern $regex.Pattern -Translation $regex.Translation

## 詳細描述

規則運算式是用來比對字元模式。Lync Server 會使用規則運算式將電話號碼在各種格式之間轉換，包括撥打的號碼、E.164，以及當地專用交換機 (PBX) 和公用交換電話網路 (PSTN) 格式。除非您學過規則運算式的使用語法及格式規則，否則可能會不知從何開始定義這些轉換規則。**New-CsVoiceRegex** Cmdlet 會提供數個參數，讓您指定特定準則，然後為您產生規則運算式。

此 Cmdlet 可協助您產生規則運算式，以做為正規化規則 (**New-CsVoiceNormalizationRule** Cmdlet) 和外撥轉譯規則 (**New-CsOutboundTranslationRule** Cmdlet) 的 Pattern 與 Translation 值，以及語音路由 (**New-CsVoiceRoute** Cmdlet) 的 NumberPattern 值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsVoiceRegex** Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoiceRegex"}

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
<td><p><em>AtLeastLength</em></p></td>
<td><p>必要</p></td>
<td><p>System.Int32</p></td>
<td><p>字串 (電話號碼) 若要符合運算式，必須達到的長度下限。例如，如果您定義的正規化規則只適用於至少有 7 位數 (或字元) 的號碼，請為此參數指定 7。</p>
<p>您必須為此參數或 ExactLength 參數輸入一個值。不能同時為這兩者輸入值。</p></td>
</tr>
<tr class="even">
<td><p><em>ExactLength</em></p></td>
<td><p>必要</p></td>
<td><p>System.Int32</p></td>
<td><p>字串 (電話號碼) 若要符合規則運算式，必須具有的長度。例如，如果您想要正規化規則只適用於 10 位數號碼，請為此參數指定 10。</p>
<p>您必須為此參數或 AtLeastLength 參數輸入一個值。不能同時為這兩者輸入值。</p></td>
</tr>
<tr class="odd">
<td><p><em>DigitsToPrepend</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>字串，指定要在電話號碼開頭新增的字元或數字。為此參數輸入的值將影響 Translation 值，影響方式為在符合規則運算式 Pattern 的號碼前面加上字元。例如，如果符合模式的號碼為 5551212，而 DigitsToPrepend 值為 425，則轉譯的號碼將為 4255551212 (假設未套用任何其他轉譯)。</p></td>
</tr>
<tr class="even">
<td><p><em>DigitsToStrip</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>要從字串 (電話號碼) 開頭除去的字元數。例如，如果輸入號碼 2065551212，而 DigitsToStrip 為 3，則號碼將轉譯為 5551212</p></td>
</tr>
<tr class="odd">
<td><p><em>StartsWith</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>字串 (電話號碼) 的第一個字元。字串除非是以 StartsWith 參數中指定的字串開頭，否則將不會符合規則運算式。例如，如果為 StartsWith 指定 &quot;+1&quot;，則只有以 +1 開頭的號碼會符合此模式並受到轉譯。請注意，StartsWith 字串中的字元數將加到 ExactLength 與 AtLeastLength 總計中。例如，如果您已將 ExactLength 指定為 10，並將 StartsWith 字串指定為 +1，則符合的電話號碼將為 8 個字元長，加上最前面的 +1 後才總共有 10 位數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

建立 Microsoft.Rtc.Management.Voice.OcsVoiceRegex 類型的物件。

## 請參閱

#### 其他資源

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[New-CsVoiceRoute](new-csvoiceroute.md)

