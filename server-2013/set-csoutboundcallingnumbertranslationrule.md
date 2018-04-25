---
title: Set-CsOutboundCallingNumberTranslationRule
TOCTitle: Set-CsOutboundCallingNumberTranslationRule
ms:assetid: e9a7190a-a50d-4d01-8f33-66ed88a52b9e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205400(v=OCS.15)
ms:contentKeyID: 49292687
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsOutboundCallingNumberTranslationRule

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的外撥電話號碼轉譯規則。外撥電話號碼轉譯規則會將 Lync Server 2013 所使用的 E.164 電話號碼，轉換成不支援 E.164 號碼之對等主幹所使用的格式。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsOutboundCallingNumberTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsOutboundCallingNumberTranslationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會變更 Identity 為 site:Redmond/SevenDigit 之撥出電話號碼轉譯規則的 Priority。在此範例中，Priority 設為 0。

    Set-CsOutboundCallingNumberTranslationRule -Identity "site:Redmond/SevenDigit" -Priority 0

## 詳細描述

外撥電話號碼轉譯規則可將 Lync 2013 所使用的 E.164 電話號碼，轉換成不支援 E.164 號碼之對等主幹所使用的格式。建立轉譯規則時，必須提供代表外撥 E.164 號碼的規則運算式 (即 Pattern)，以及代表轉換後之號碼 (即 Translation) 的規則運算式。

外撥電話號碼轉譯規則必須和主幹組態設定相連結。當您建立新的轉譯規則時，必須同時指定主幹組態設定的 Identity 與新規則的名稱 (例如 site:Redmond/RedmondTranslationRule)。請注意，建立新規則時未必一定要有主幹組態設定。例如，假設您要建立規則 site:Redmond/RedmondTranslationRule，但還未建立 Remond 網站的主幹組態設定。若 Redmond 網站為有效的網站，將會自動為該網站建立主幹組態設定，並將新的轉譯規則指派給該設定集合。但 Redmond 網站若是不存在，命令將會失敗。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsOutboundCallingNumberTranslationRule"}

**Lync Server 控制台：**若要使用 Lync Server 控制台編輯現有的撥出電話號碼轉譯規則，請依序按一下 \[語音路由\] 及 \[主幹組態\]，然後按兩下含有要修改之規則的組態設定。在 \[編輯主幹組態\] 對話方塊中，向下捲動至標示電話號碼轉譯規則的區段，然後按兩下要修改的規則。

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
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓系統管理員提供轉譯規則隨附的其他文字。此描述可用來協助系統管理員清楚識別規則的目的。</p></td>
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
<td><p>要修改之轉譯規則的唯一識別碼。Identity 是由範圍後面加上在每個範圍內的唯一名稱所組成。例如：</p>
<p>-Identity &quot;site:Redmond/OutboundRule1&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參照傳遞給 Cmdlet，而不設定個別參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>Pattern</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>規則運算式，表示 Translation 將套用的號碼模式。</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>指派給規則的優先順序。如果號碼符合多個外撥轉譯規則的 Pattern，將根據優先順序套用規則。會按照規則的指定優先順序來處理規則；第一個要處理的規則具有優先順序 0；第二個要處理的規則具有優先順序 1；依此類推。</p></td>
</tr>
<tr class="even">
<td><p><em>Translation</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>規則運算式，將套用至符合 Pattern 的號碼，使號碼準備好以便撥出電話。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Set-CsOutboundCallingNumberTranslationRule** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.CallingNumberTranslationRule\#Decorated 物件執行個體

## 傳回類型

無。反之，**Set-CsOutboundCallingNumberTranslationRule** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.CallingNumberTranslationRule\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsOutboundCallingNumberTranslationRule](get-csoutboundcallingnumbertranslationrule.md)  
[New-CsOutboundCallingNumberTranslationRule](new-csoutboundcallingnumbertranslationrule.md)  
[Remove-CsOutboundCallingNumberTranslationRule](remove-csoutboundcallingnumbertranslationrule.md)

