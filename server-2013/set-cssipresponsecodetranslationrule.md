---
title: Set-CsSipResponseCodeTranslationRule
TOCTitle: Set-CsSipResponseCodeTranslationRule
ms:assetid: 3ce2fafe-9c79-4462-9f24-c2a30502e641
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425895(v=OCS.15)
ms:contentKeyID: 49290664
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsSipResponseCodeTranslationRule

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的 SIP 回應碼轉譯規則。這些規則可讓系統管理員將介於 400 到 699 之間的 SIP 回應碼對應到 Lync Server 所使用的值。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsSipResponseCodeTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsSipResponseCodeTranslationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Priority <Int32>] [-ReceivedISUPCauseValue <Int32>] [-ReceivedResponseCode <Int32>] [-TranslatedResponseCode <Int32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改 Identity 為 PstnGateway:192.168.0.240/Rule404 之轉譯規則的 ReceivedISUPCauseValue 內容。

    Set-CsSipResponseCodeTranslationRule -Identity "PstnGateway:192.168.0.240/Rule404" -ReceivedISUPCauseValue 477

## 範例 2

範例 2 會將 Identity 為 PstnGateway:192.168.0.240/Rule404 的轉譯規則標示為優先順序最高的規則；亦即，將優先處理此規則。只要將 Priority 設為 0 即可。

    Set-CsSipResponseCodeTranslationRule -Identity "PstnGateway:192.168.0.240/Rule404" -Priority 0

## 範例 3

範例 3 顯示如何將設定供組織使用之所有轉譯規則的 ReceivedISUPCauseValue 內容設為 -1；這將導致進行轉譯規則時忽略 ISUP 原因碼。為達成此目的，命令會先呼叫 **Get-CsSipResponseCodeTranslationRule** Cmdlet 而不搭配任何參數，以傳回目前使用中的所有 SIP 回應碼轉譯規則的集合。然後，將該集合管線傳送到 **Set-CsSipResponseCodeTranslationRule** Cmdlet，由其修改集合中每一個項目的 ReceivedISUPCauseValue 內容。

    Get-CsSipResponseCodeTranslationRule | Set-CsSipResponseCodeTranslationRule -ReceivedISUPCauseValue -1

## 詳細描述

SIP 主幹連線可連接 Voice over Internet Protocol (VoIP) 網路 (例如 Enterprise Voice) 與公用交換電話網路 (PSTN)。在 Lync Server 中，中繼伺服器 使用對等主幹與 PSTN 網路互動。PSTN 網路上的撥出電話無法作用時，系統會自動產生 ISDN User Part (ISUP) 原因碼。例如，PSTN 閘道可能傳送原因碼 34，代表沒有可用的電路或通訊管道可以完成通話。中繼伺服器對等主幹端收到 ISUP 原因碼時，會將原因碼轉換為 SIP 回應碼，並且將這個回應碼傳送給中繼伺服器本身。接著，Lync Server 會使用這些回應碼做出輸出路由的決定。例如，不正常的閘道可能自動被指派為「非慣用」狀態；如此一來可以將不正常閘道的使用者數量降至最少，因此可以大幅提高成功完成通話的機率。

但是，並非所有閘道都使用建議的 ISUP 原因碼，對應 Lync Server 使用的 SIP 回應碼。針對這類閘道，系統管理員可以使用 **CsSipResponseCodeTranslationRule** Cmdlet，將閘道 SIP 回應碼 (如果有 ISUP 原因碼，則二者結合) 對應到 Lync Server 使用的 SIP 回應碼。例如，閘道可能將 ISUP 原因碼 34 (「沒有可用的電路/通訊管道」) 對應到 SIP 回應碼 486 (「忙碌中」)。根據回應碼 486，Lync Server 的輸出路由邏輯不會嘗試找出新閘道以完成通話。

但是，如果是 Lync Server，該 SIP 回應碼 486 則會被對應到 SIP 回應碼 503。回應碼 503 會觸發 Lync Server 的輸出路由邏輯中的重試機制；這代表系統會試著找出另一個閘道以完成通話。為了處理這種情況，您可以建立轉譯規則，將 ISUP 原因碼 34 和 SIP 回應碼 486 的組合對應到 SIP 回應碼 503。

**Set-CsSipResponseCodeTranslationRule** Cmdlet 提供一種方法，讓您修改先前為在組織中使用而設定的任何轉譯規則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsSipResponseCodeTranslationRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsSipResponseCodeTranslationRule"}

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
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之轉譯規則的唯一識別碼。轉譯規則的 Identity 由兩個部分組成：設定規則的範圍，以及建立規則時指定的規則名稱。例如，在全域範圍建立，且名稱為 Rule404 之轉譯規則的 Identity 會類似如下：global/Rule404。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>整數</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>轉譯規則的相對優先順序。會按照規則的指定優先順序來處理規則；第一個要處理的規則具有優先順序 0；第二個要處理的規則具有優先順序 1；依此類推。</p></td>
</tr>
<tr class="even">
<td><p><em>ReceivedISUPCauseValue</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>必須出現在 SIP 回應訊息中的 ISDN User Part (ISUP) 原因碼值，當閘道回應 IMVITE 訊息時，會使用該值。值 -1 指出執行轉譯規則時，只會使用 SIP 回應碼；將忽略 ISUP 原因碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReceivedResponseCode</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>當閘道回應 INVITE 訊息時，將使用的 SIP 回應碼值。回應碼可以是介於 400 和 699 (含) 之間的任何整數值。雖然此 Cmdlet 接受小於 400 的整數值，但不會將它們視為最終回應。因此，永遠不會使用轉譯規則。值 0 表示執行轉譯規則時，只會使用 ISUP 原因碼；將忽略 SIP 回應碼。</p></td>
</tr>
<tr class="even">
<td><p><em>TranslatedResponseCode</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>ReceivedResponseCode 和/或 ReceivedISUPCauseCode 應該轉譯成的 SIP 回應碼值。轉譯後的回應碼可以是介於 400 和 699 (含) 之間的任何整數值。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.SipResponseCodeTranslationRule\#Decorated 物件。**Set-CsSipResponseCodeTranslationRule** Cmdlet 接受 SIP 回應碼轉譯規則物件管線傳送的執行個體。

## 傳回類型

**Set-CsSipResponseCodeTranslationRule** Cmdlet 不會傳回任何物件或值。而是此 Cmdlet 會修改 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsSipResponseCodeTranslationRule](get-cssipresponsecodetranslationrule.md)  
[New-CsSipResponseCodeTranslationRule](new-cssipresponsecodetranslationrule.md)  
[Remove-CsSipResponseCodeTranslationRule](remove-cssipresponsecodetranslationrule.md)

