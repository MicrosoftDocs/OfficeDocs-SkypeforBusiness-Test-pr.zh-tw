---
title: Get-CsOutboundCallingNumberTranslationRule
TOCTitle: Get-CsOutboundCallingNumberTranslationRule
ms:assetid: 65589388-f935-4d25-ae74-362be97c8597
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204962(v=OCS.15)
ms:contentKeyID: 49291137
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsOutboundCallingNumberTranslationRule

 

_**上次修改主題的時間：** 2015-03-09_

傳回建立供組織使用之外撥電話號碼轉譯規則的資訊。外撥電話號碼轉譯規則可將 Lync Server 2013 所使用的 E.164 電話號碼，轉換成不支援 E.164 號碼之對等主幹所使用的格式。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsOutboundCallingNumberTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsOutboundCallingNumberTranslationRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回目前設定供組織使用之所有外撥電話號碼轉譯規則的資訊。

    Get-CsOutboundCallingNumberTranslationRule

## 範例 2

在範例 2 中，只會針對 Identity 為 "site:Redmond/SevenDigit" 的外撥電話號碼轉譯規則傳回資訊。

    Get-CsOutboundCallingNumberTranslationRule -Identity "site:Redmond/SevenDigit"

## 範例 3

範例 3 會針對為 Redmond 網站設定的所有外撥電話號碼轉譯規則傳回資訊。作法是將 Identity 參數的值設為 Redmond 網站的 Identity (site:Redmond)。

    Get-CsOutboundCallingNumberTranslationRule -Identity "site:Redmond"

## 範例 4

範例 4 所示的命令只會傳回位在 Redmond 網站上，Priority 等於 0 之外撥電話號碼轉譯規則的資訊。為達成此目的，命令會先使用 **Get-CsOutboundCallingNumberTranslationRule** Cmdlet 和 Identity 參數，以傳回指派給 Redmond 網站之所有轉譯規則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Priority 等於 0 的規則。

    Get-CsOutboundCallingNumberTranslationRule -Identity "site:Redmond" | Where-Object {$_.Priority -eq 0}

## 詳細描述

外撥電話號碼轉譯規則可將 Lync 2013 所使用的 E.164 電話號碼，轉換成不支援 E.164 號碼之對等主幹所使用的格式。建立轉譯規則時，必須提供代表外撥 E.164 號碼的規則運算式 (即 Pattern)，以及代表轉換後號碼的規則運算式 (即 Translation)。

外撥電話號碼轉譯規則必須和主幹組態設定相連結。當您建立新的轉譯規則時，必須同時指定主幹組態設定的 Identity 與新規則的名稱 (例如 site:Redmond/RedmondTranslationRule)。請注意，建立新規則時未必一定要有主幹組態設定。例如，假設您要建立規則 site:Redmond/RedmondTranslationRule，但還未建立 Remond 網站的主幹組態設定。若 Redmond 網站為有效的網站，將會自動為該網站建立主幹組態設定，並將新的轉譯規則指派給該設定集合。但 Redmond 網站若是不存在，命令將會失敗。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsOutboundCallingNumberTranslationRule"}

**Lync Server 控制台：**若要檢視 Lync Server 控制台中的外撥電話號碼轉譯規則，請按一下 \[語音路由\]，然後再按一下 \[主幹組態\]。在 \[名稱\] 欄中按兩下適當的項目，然後在 \[編輯主幹組態\] 對話方塊中，向下捲動至標示來電號碼轉譯規則的部分。

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>執行萬用字元搜尋，可讓您只傳回 Identity 符合萬用字元字串的那些外撥轉譯規則。例如，下列語法會傳回包含 &quot;Redmond&quot; 字串值的所有轉譯規則：</p>
<p>-Filter &quot;*Redmond*&quot;</p>
<p>若要傳回在網站範圍設定的所有轉譯規則，請使用下列語法：</p>
<p>-Filter &quot;site:*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要擷取之外撥電話號碼轉譯規則的唯一識別碼。Identity 是由範圍後面加上每個範圍內的唯一名稱所組成；例如：</p>
<p>-Identity &quot;site:Redmond/OutboundRule1&quot;</p>
<p>若要傳回為特定範圍 (例如 Redmond 網站) 設定的所有轉譯規則，直接將 Identity 設為範圍本身即可：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>如果 Identity 參數和 Filter 參數都沒有指定，<strong>Get-CsOutboundCallingNumberTranslationRule</strong> Cmdlet 就會傳回所有外撥電話號碼轉譯規則的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取外撥電話號碼轉譯規則資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsOutboundCallingNumberTranslationRule** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsOutboundCallingNumberTranslationRule** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.CallingNumberTranslationRule\#Decorated 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsOutboundCallingNumberTranslationRule](new-csoutboundcallingnumbertranslationrule.md)  
[Remove-CsOutboundCallingNumberTranslationRule](remove-csoutboundcallingnumbertranslationrule.md)  
[Set-CsOutboundCallingNumberTranslationRule](set-csoutboundcallingnumbertranslationrule.md)

