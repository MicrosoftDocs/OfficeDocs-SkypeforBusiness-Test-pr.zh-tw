---
title: Test-CsDialPlan
TOCTitle: Test-CsDialPlan
ms:assetid: e6618394-82c5-4bc2-85cc-97ac4686a1aa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399024(v=OCS.15)
ms:contentKeyID: 49292635
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsDialPlan

 

_**上次修改主題的時間：** 2015-03-09_

根據撥號對應表 (舊名為位置設定檔) 測試電話號碼，然後傳回要套用到該號碼的正規化規則，以及套用正規化規則加以轉譯後的號碼。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsDialPlan -DialedNumber <PhoneNumber> -Dialplan <LocationProfile>

## 範例

## 範例 1

本例會針對 Identity 為 site:Redmond 的撥號對應表執行測試。首先執行 **Get-CsDialPlan** Cmdlet，以擷取 Identity 為 site:Redmond 的撥號對應表。接著，該撥號對應表物件便傳送至 **Test-CsDialPlan** Cmdlet，在此會針對電話號碼 14255559999 測試撥號對應表。輸出將是語音正規化規則之後的 DialedNumber，並套用符合模式。如果在網站內有多個具有符合模式的正規化規則，則會套用 Priority 值最低的規則。如果沒有規則的模式符合 DialedNumber 值 (例如，如果正規化規則符合 11 位數號碼的模式，而您提供 7 位數的號碼)，則不會傳回任何值。

這個命令的輸出包含電話號碼以及正規化規則。正規化規則有許多屬性，且此輸出預設會以省略符號截斷 (...)。為了查看傳回之語音正規化規則的所有屬性和值，我們先將輸出傳送至 **Format-List** Cmdlet，然後顯示在螢幕上。這會在個別行上列出電話號碼及正規化規則，而正規化規則屬性和值將會換行，以符合螢幕大小。

    Get-CsDialPlan -Identity site:Redmond | Test-CsDialPlan -DialedNumber 14255559999 | Format-List

## 範例 2

範例 2 與範例 1 相同，只是它不會直接將 Get 作業的結果傳送至 **Test-CsDialPlan** Cmdlet，而是會先將物件儲存在變數 $a 中，然後以值的形式傳遞到 DialPlan 參數，當作對其執行測試的撥號對應表來使用。

如同範例 1，我們在這個命令的結束處，將輸出管線傳送到 **Format-List** Cmdlet，因此可以看到比預設更多的語音正規化規則的資訊。

    $a = Get-CsDialPlan -Identity site:Redmond
    Test-CsDialPlan -DialedNumber 14255559999 -Dialplan $a | Format-List

## 範例 3

此範例會對 Lync Server 部署內定義的所有撥號對應表執行撥號對應表測試。首先會執行 **Get-CsDialPlan** Cmdlet (不含參數)，以擷取所有撥號對應表。傳回的撥號對應表集合便會傳送至 **Test-CsDialPlan** Cmdlet，其中集合中的每個撥號對應表都會針對電話號碼 2065559999 進行測試。輸出會是已套用語音正規化規則的轉譯號碼清單，且集合中的每個撥號對應表有一份清單。如果撥號對應表內沒有任何語音正規化規則套用至特定撥號對應表的 DialedNumber 值 (例如，如果正規化規則符合 11 位數號碼的模式，而您提供 7 位數的號碼)，則會在該撥號對應表的清單中出現空白行。

根據預設，輸出會截斷已套用之語音正規化規則的完整顯示。在範例 1 和 2 中，我們能夠檢視整個輸出，方法是將測試結果管線傳送到 **Format-List** Cmdlet。此範例會將輸出管線傳送到 **Format-Table** Cmdlet 搭配 Wrap 參數。這會以表格格式顯示每個項目 (一欄為轉譯的號碼，一欄為套用的語音正規化規則)，但會將輸出換行，因此正規化規則會在欄內換行。

    Get-CsDialPlan | Test-CsDialPlan -DialedNumber 2065559999 | Format-Table -Wrap

## 詳細描述

這個 Cmdlet 允許您查看將撥號對應表套用到特定電話號碼後的結果。撥號對應表提供可讓 Enterprise Vioce 使用者撥打電話所需的資訊 (包括如何套用正規化規則)。只要有撥打的號碼和撥號對應表，這個 Cmdlet 會驗證將套用撥號對應表內的哪個正規化規則，以及轉譯後的號碼。

您可以使用此 Cmdlet 來疑難排解號碼轉譯的問題，或是驗證規則對特定號碼的應用。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsDialPlan** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsDialPlan"}

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
<td><p>PhoneNumber</p></td>
<td><p>您想要用來測試撥號對應表的電話號碼，會在 Dialplan 參數中指定。</p>
<p>完整資料類型：Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
</tr>
<tr class="even">
<td><p><em>Dialplan</em></p></td>
<td><p>必要</p></td>
<td><p>LocationProfile</p></td>
<td><p>包含撥號對應表參照的物件，您想要用此撥號對應表來測試 DialedNumber 參數中所指定的號碼。</p>
<p>完整資料類型：Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile 物件。接受撥號對應表物件管線傳送的輸入。

## 傳回類型

傳回 Microsoft.Rtc.Management.Voice.LocationProfileTestResult 類型的物件。

## 請參閱

#### 其他資源

[New-CsDialPlan](new-csdialplan.md)  
[Remove-CsDialPlan](remove-csdialplan.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Grant-CsDialPlan](grant-csdialplan.md)

