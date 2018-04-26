---
title: New-CsSipResponseCodeTranslationRule
TOCTitle: New-CsSipResponseCodeTranslationRule
ms:assetid: f7667ffd-3d11-40ec-87d4-7f9b1a861aae
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413041(v=OCS.15)
ms:contentKeyID: 49292841
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipResponseCodeTranslationRule

 

_**上次修改主題的時間：** 2015-03-09_

建立新的 SIP 回應碼轉譯規則。這些規則可讓系統管理員將介於 400 到 699 的 SIP 回應碼值對應到 Lync Server 使用的值。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsSipResponseCodeTranslationRule -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsSipResponseCodeTranslationRule -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -TranslatedResponseCode <Int32> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Priority <Int32>] [-ReceivedISUPCauseValue <Int32>] [-ReceivedResponseCode <Int32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示之命令會建立新的 SIP 回應碼轉譯規則，Identity 為 PstnGateway:192.168.0.240/Rule404。這個規則會將接收的回應碼 434 轉譯為標準 SIP 回應碼 404 (找不到)。

    New-CsSipResponseCodeTranslationRule -Identity "PstnGateway:192.168.0.240/Rule404" -ReceivedResponseCode 434 -TranslatedResponseCode 404

## 範例 2

範例 2 中所示之命令會執行與範例 1 所示之命令的相同工作。但是，在範例 2 中，系統使用 Parent 和 Name 參數，而非 Identity 參數。這僅代表建立新 SIP 回應碼轉譯規則 (其 Identity 為 PstnGateway:192.168.0.240/Rule404) 的替代方式。

    New-CsSipResponseCodeTranslationRule -Parent "PstnGateway:192.168.0.240" -Name "Rule404" -ReceivedResponseCode 434 -TranslatedResponseCode 404

## 詳細描述

SIP 主幹連線可連接 Voice over Internet Protocol (VoIP) 網路 (例如 Enterprise Voice) 與公用交換電話網路 (PSTN)。在 Lync Server 中，中繼伺服器 使用對等主幹與 PSTN 網路互動。PSTN 網路上的撥出電話無法作用時，系統會自動產生 ISDN User Part (ISUP) 原因碼。例如，PSTN 閘道可能傳送原因碼 34，代表沒有可用的電路或通訊管道可以完成通話。中繼伺服器對等主幹端收到 ISUP 原因碼時，會將原因碼轉換為 SIP 回應碼，並且將這個回應碼傳送給中繼伺服器本身。接著，Lync Server 會使用這些回應碼做出輸出路由的決定。例如，不正常的閘道可能自動被指派為「非慣用」狀態；如此一來可以將不正常閘道的使用者數量降至最少，因此可以大幅提高成功完成通話的機率。

但是，並非所有閘道都使用建議的 ISUP 原因碼，對應 Lync Server 使用的 SIP 回應碼。針對這類閘道，系統管理員可以使用 **CsSipResponseCodeTranslationRule** Cmdlet，將閘道 SIP 回應碼 (如果沒有該回應碼，則結合 ISUP 原因碼) 對應到 Lync Server 使用的 SIP 回應碼。例如，閘道可能將 ISUP 原因碼 34 (「沒有可用的電路/通訊管道」) 對應到 SIP 回應碼 486 (「忙碌中」)。根據回應碼 486，Lync Server 的輸出路由邏輯不會嘗試找出新閘道以完成通話。

但是，如果是 Lync Server，該 SIP 回應碼 486 則會被對應到 SIP 回應碼 503。回應碼 503 會觸發 Lync Server 的輸出路由邏輯中的重試機制；這代表系統會試著找出另一個閘道以完成通話。為了處理這種情況，您可以建立轉譯規則，將 ISUP 原因碼 34 和 SIP 回應碼 486 的組合對應到 SIP 回應碼 503。這些新的轉譯規則是使用 **New-CsSipResponseCodeTranslationRule** Cmdlet 所建立。轉譯規則可以指派至全域範圍、網站範圍或服務範圍 (僅限 PSTN 閘道服務)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsSipResponseCodeTranslationRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipResponseCodeTranslationRule"}

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
<td><p>要建立之轉譯規則的唯一識別碼。轉譯規則的 Identity 由兩個部分組成：要指派規則的範圍，以及要給予規則的名稱。例如，在全域範圍建立的轉譯規則 Rule404，它的 Identity 如下：global/Rule404。</p>
<p>與其使用 Identity 參數，您可以改為在建立新的轉譯規則時使用 Parent 和 Name 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>用來區隔不同轉譯規則的名稱。指定範圍內的名稱必須是唯一，例如，Redmond 網站只能有一個名稱為 Rule404 的規則。但是，您可以在 Redmond 網站有名稱為 Rule404 的轉譯規則，並在 Dublin 網站也有另一個名稱為 Rule404 的規則。</p>
<p>Name 參數永遠都必須與 Parent 參數一起使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指派新轉譯規則的範圍。若要指派規則給全域範圍，請使用下列語法：-Parent global。若要指派規則給網站範圍，請使用如下語法：-Parent site:Redmond。若要指派規則給服務範圍，請使用類似下列的語法：-Parent PstnGateway:192.168.0.242。</p>
<p>Parent 參數永遠都必須與 Name 參數一起使用。</p></td>
</tr>
<tr class="even">
<td><p><em>TranslatedResponseCode</em></p></td>
<td><p>必要</p></td>
<td><p>System.Int32</p></td>
<td><p>ReceivedResponseCode 和/或 ReceivedISUPCauseCodeValue 應轉譯成的 Lync Server SIP 回應碼的值。轉譯後的回應碼可以是介於 400 和 699 (含) 之間的任何整數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>轉譯規則的相對優先順序。會按照規則的指定優先順序來處理規則；第一個要處理的規則具有優先順序 0；第二個要處理的規則具有優先順序 1；依此類推。若未指定，系統會在新規則的範圍中，給予新規則最低的優先順序。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReceivedISUPCauseValue</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>必須出現在 SIP 回應訊息中的 ISDN User Part (ISUP) 原因碼值，當閘道回應 IMVITE 訊息時，會使用該值。值 -1 指出執行轉譯規則時，只會使用 SIP 回應碼；將忽略 ISUP 原因碼。</p></td>
</tr>
<tr class="even">
<td><p><em>ReceivedResponseCode</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>當閘道回應 INVITE 訊息時，將使用的 SIP 回應碼值。回應碼可以是介於 400 和 699 (含) 之間的任何整數值。雖然此 Cmdlet 接受小於 400 的整數值，但不會將它們視為最終回應。因此，永遠不會使用轉譯規則。值 0 表示執行轉譯規則時，只會使用 ISUP 原因碼；將忽略 SIP 回應碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsSipResponseCodeTranslationRule** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsSipResponseCodeTranslationRule** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.SipResponseCodeTRanslationRule\#Decorated 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsSipResponseCodeTranslationRule](get-cssipresponsecodetranslationrule.md)  
[Remove-CsSipResponseCodeTranslationRule](remove-cssipresponsecodetranslationrule.md)  
[Set-CsSipResponseCodeTranslationRule](set-cssipresponsecodetranslationrule.md)

