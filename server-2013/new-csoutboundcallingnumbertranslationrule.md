---
title: New-CsOutboundCallingNumberTranslationRule
TOCTitle: New-CsOutboundCallingNumberTranslationRule
ms:assetid: 959591bb-4a6b-4b7f-9666-da1fa0f9cd43
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205097(v=OCS.15)
ms:contentKeyID: 49291714
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsOutboundCallingNumberTranslationRule

 

_**上次修改主題的時間：** 2015-03-09_

建立新的外撥電話號碼轉譯規則。外撥電話號碼轉譯規則會將 Lync Server 2013 所使用的 E.164 電話號碼，轉換成不支援 E.164 號碼之對等主幹所使用的格式。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsOutboundCallingNumberTranslationRule -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsOutboundCallingNumberTranslationRule -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立新的外撥電話號碼轉譯規則，此規則會將以 +1206 字串值為開頭的 E.164 號碼 (例如 +12065551219)，轉換成 7 位數的值 (例如 5551219，去掉了 +1206)。

    New-CsOutboundCallingNumberTranslationRule -Parent "site:Redmond" -Name SevenDigit -Description "Converts a dialed number to seven digits" -Pattern '^\+1206(\d{7})$' -Translation '$1'

## 詳細描述

外撥電話號碼轉譯規則可將 Lync 2013 所使用的 E.164 電話號碼，轉換成不支援 E.164 號碼之對等主幹所使用的格式。建立轉譯規則時，必須提供規則運算式代表外撥的 E.164 號碼 (即 Pattern)，以及代表轉換後之號碼 (即 Translation) 的規則運算式。

外撥電話號碼轉譯規則必須和主幹組態設定相連結。當您建立新的轉譯規則時，必須同時指定主幹組態設定的 Identity 與新規則的名稱 (例如 site:Redmond/RedmondTranslationRule)。請注意，建立新規則時未必一定要有主幹組態設定。例如，假設您要建立規則 site:Redmond/RedmondTranslationRule，但還未建立 Remond 網站的主幹組態設定。若 Redmond 網站為有效的網站，將會自動為該網站建立主幹組態設定，並將新的轉譯規則指派給該設定集合。但 Redmond 網站若是不存在，命令將會失敗。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsOutboundCallingNumberTranslationRule"}

**Lync Server 控制台：**若要使用 Lync Server 控制台來建立外撥電話號碼轉譯規則，請依序按一下 \[語音路由\] 和 \[主幹組態\]，然後在 \[名稱\] 欄中按兩下適當的項目。在 \[編輯主幹組態\] 對話方塊中，向下捲動至標示來電號碼轉譯規則的部分，然後按一下 \[新增\]。

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
<td><p>新轉譯規則的唯一識別碼。名稱中包含範圍 (父項)、&quot;/&quot; 字元，以及該範圍中的唯一名稱。例如，為 Redmond 網站建立名為 RedmondDialing 的規則，其 Identity 看起來如下：</p>
<p>-Identity &quot;site:Redmond/RedmondDialing&quot;</p>
<p>若您使用 Identity 參數，命令就不能包含 Parent 或 Name 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>新轉譯規則的名稱；必須是給定範圍內的唯一名稱。例如：</p>
<p>-Name &quot;RedmondDialing&quot;</p>
<p>在任何時候使用 Name 參數時，也必須使用 Parent 參數。Name 參數不能用在與 Identity 參數相同的命令中。</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要設定新轉譯規則的範圍。若要在全域範圍設定規則，請使用下列語法：</p>
<p>-Parent &quot;global&quot;</p>
<p>若要在網站範圍設定規則，請使用類似下列的語法：</p>
<p>-Parent &quot;site:Redmond&quot;</p>
<p>若要在服務範圍 (僅限 PstnGateway 服務) 設定規則，請使用類似下列的語法：</p>
<p>-Parent &quot;service:PstnGateway:192.168.0.100&quot;</p>
<p>在任何時候使用 Parent 參數時，也必須使用 Name 參數。Parent 參數不能用在與 Identity 參數相同的命令中。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓系統管理員提供隨附轉譯規則的其他文字。此描述可用來協助系統管理員清楚識別規則的用途。</p></td>
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
<td><p>建立物件參照，而不需實際認可該物件為永久變更。如果您會將利用此參數呼叫之 Cmdlet 的輸出指派給變數，則可變更物件參照的屬性，然後呼叫此 Cmdlet 相符的 Set- Cmdlet 來認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>Pattern</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>規則運算式，表示將套用於 Translation 的號碼模式。</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>指派給規則的優先順序。若號碼符合多個外撥轉譯規則的 Pattern，將根據優先順序套用規則。會按照規則的指定優先順序來處理規則；第一個要處理的規則具有優先順序 0；第二個要處理的規則具有優先順序 1；依此類推。</p></td>
</tr>
<tr class="even">
<td><p><em>Translation</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>規則運算式，將套用至符合 Pattern 的號碼，以備妥該號碼供輸出來電。</p></td>
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

無。**New-CsOutboundCallingNumberTranslationRule** Cmdlet 不接受管線傳送的資料。

## 傳回類型

**New-CsOutboundCallingNumberTranslationRule** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.CallingNumberTranslationRule\#Decorated 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsOutboundCallingNumberTranslationRule](get-csoutboundcallingnumbertranslationrule.md)  
[Remove-CsOutboundCallingNumberTranslationRule](remove-csoutboundcallingnumbertranslationrule.md)  
[Set-CsOutboundCallingNumberTranslationRule](set-csoutboundcallingnumbertranslationrule.md)

