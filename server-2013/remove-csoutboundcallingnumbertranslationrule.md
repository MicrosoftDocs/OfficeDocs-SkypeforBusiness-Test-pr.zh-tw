---
title: Remove-CsOutboundCallingNumberTranslationRule
TOCTitle: Remove-CsOutboundCallingNumberTranslationRule
ms:assetid: 41ca92c9-7c2e-44e0-8ec8-9f39843b73e7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204836(v=OCS.15)
ms:contentKeyID: 49290723
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsOutboundCallingNumberTranslationRule

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的多撥電話號碼轉譯規則。外撥電話號碼轉譯規則會將 Lync Server 2013 所使用的 E.164 電話號碼，轉換成不支援 E.164 號碼之對等主幹所使用的格式。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsOutboundCallingNumberTranslationRule -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除 Identity 為 site:Redmond/SevenDigit 的外撥電話號碼轉譯規則。

    Remove-CsOutboundCallingNumberTranslationRule -Identity "site:Redmond/SevenDigit"

## 範例 2

範例 2 會移除為 Redmond 網站設定的所有外撥電話號碼轉譯規則。為達成此目的，命令會呼叫 **Remove-CsOutboundCallingNumberTranslationRule** Cmdlet 並搭配 Identity 參數；參數值 "site:Redmond" 可確保所有為 Redmond 網站設定的轉譯規則皆被移除。

    Remove-CsOutboundCallingNumberTranslationRule -Identity "site:Redmond"

## 範例 3

範例 3 會刪除使用 Pattern 為 "^\\+1425(\\d{7})$" 的所有外撥電話號碼轉譯規則。為達成此目的，命令會先使用 **Get-CsOutboundCallingNumberTranslationRule** Cmdlet，以傳回組織中使用的所有轉譯規則集合。然後，此集合會管線傳送到 Where-Object Cmdlet，這會只挑出 Pattern 屬性等於 "^\\+1425(\\d{7})$" 的規則。接著將篩選後的集合管線傳送到 **Remove-CsOutboundCallingNumberTranslationRule** Cmdlet，以刪除集合中的每個規則。

    Get-CsOutboundCallingNumberTranslationRule | Where-Object {$_.Pattern -eq '^\+1425(\d{7})$'} | Remove-CsOutboundCallingNumberTranslationRule

## 詳細描述

外撥電話號碼轉譯規則可將 Lync 2013 所使用的 E.164 電話號碼，轉譯成不支援 E.164 號碼之對等主幹所使用的格式。建立轉譯規則時，必須提供規則運算式代表外撥的 E.164 號碼 (即 Pattern)，以及代表轉換後之號碼 (即 Translation) 的規則運算式。

外撥電話號碼轉譯規則必須和主幹組態設定相連結。當您建立新的轉譯規則時，必須同時指定主幹組態設定的 Identity 與新規則的名稱 (例如 site:Redmond/RedmondTranslationRule)。請注意，建立新規則時未必一定要有主幹組態設定。例如，假設您要建立規則 site:Redmond/RedmondTranslationRule，但還未建立 Remond 網站的主幹組態設定。若 Redmond 網站為有效的網站，將會自動為該網站建立主幹組態設定，並將新的轉譯規則指派給該設定集合。但 Redmond 網站若是不存在，命令將會失敗。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsOutboundCallingNumberTranslationRule"}

**Lync Server 控制台：**若要使用 Lync Server 控制台來移除外撥電話號碼轉譯規則，請按一下 \[語音路由\]，然後再按一下 \[主幹組態\]。在 \[名稱\] 欄中按兩下適當的項目，然後在 \[編輯主幹組態\] 對話方塊中，向下捲動至標示來電號碼轉譯角色的部分。選取所要刪除的規則，然後按一下 \[移除\]。

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
<td><p>您要移除之外撥轉譯規則的唯一識別碼。Identity 是由範圍加上每個範圍中的唯一名稱組成。例如：</p>
<p>-Identity &quot;site:Redmond/OutboundRule1&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Remove-CsOutboundCallingNumberTranslationRule** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.CallingNumberTranslationRule\#Decorated 物件執行個體。

## 傳回類型

無。反之，**Remove-CsOutboundCallingNumberTranslationRule** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.CallingNumberTranslationRule\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsOutboundCallingNumberTranslationRule](get-csoutboundcallingnumbertranslationrule.md)  
[New-CsOutboundCallingNumberTranslationRule](new-csoutboundcallingnumbertranslationrule.md)  
[Set-CsOutboundCallingNumberTranslationRule](set-csoutboundcallingnumbertranslationrule.md)

