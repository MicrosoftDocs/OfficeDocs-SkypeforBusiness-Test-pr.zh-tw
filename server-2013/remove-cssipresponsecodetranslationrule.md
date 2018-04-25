---
title: Remove-CsSipResponseCodeTranslationRule
TOCTitle: Remove-CsSipResponseCodeTranslationRule
ms:assetid: beb5f508-5f90-46ee-b5c5-7da8781420e0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412932(v=OCS.15)
ms:contentKeyID: 49292178
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsSipResponseCodeTranslationRule

 

_**上次修改主題的時間：** 2015-03-09_

移除 SIP 回應碼轉譯規則。這些規則可讓系統管理員將介於 400 到 699 的 SIP 回應碼值對應到 Lync Server 使用的值。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsSipResponseCodeTranslationRule -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除單一回應碼轉譯規則：規則的 Identity 為 PstnGateway:192.168.0.240/Rule404。

    Remove-CsSipResponseCodeTranslationRule -Identity "PstnGateway:192.168.0.240/Rule404"

## 範例 2

範例 2 會移除 PSTN 閘道 192.168.0.240 的所有回應碼轉譯規則。為達成此目的，命令會先呼叫 **Get-CsSipResponseCodeTranslationRule** Cmdlet 搭配 Filter 參數；篩選值 "service:PstnGateway:192.168.0.240/\*" 可將傳回的資料限制在 Identity 開頭為字串值 "service:PstnGateway:192.168.0.240/" 的規則。然後將此篩選後的集合管線傳送到 **Remove-CsSipResponseTranslationCode** Cmdlet，以刪除集合中的每一個規則。

    Get-CsSipResponseCodeTranslationRule -Filter "service:PstnGateway:192.168.0.240/*" | Remove-CsSipResponseTranslationCode

## 範例 3

範例 3 會刪除所有 ReceivedISUPCauseValue 屬性尚未設定值的回應碼轉譯規則。為為達成此目的，命令會先呼叫不含任何參數的 **Get-CsSipResponseCodeTranslationRule** Cmdlet，以傳回目前使用之所有回應碼轉譯規則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 ReceivedISUPCauseValue 屬性等於 -1 的規則。

接著將篩選後的集合管線傳送到 **Remove-CsSipResponseTranslationCode** Cmdlet，以刪除集合中的每一個規則。

    Get-CsSipResponseCodeTranslationRule | Where-Object {$_.ReceivedISUPCauseValue -eq -1} | Remove-CsSipResponseTranslationCode

## 詳細描述

SIP 主幹連線可連接 Voice over Internet Protocol (VoIP) 網路 (例如 Enterprise Voice) 與公用交換電話網路 (PSTN)。在 Lync Server 中，中繼伺服器使用對等主幹與 PSTN 網路互動。PSTN 網路上的撥出電話無法作用時，系統會自動產生 ISDN User Part (ISUP) 原因碼。例如，PSTN 閘道可能傳送原因碼 34，代表沒有可用的電路或通訊管道可以完成通話。中繼伺服器對等主幹端收到 ISUP 原因碼時，會將原因碼轉換為 SIP 回應碼，並且將這個回應碼傳送給中繼伺服器本身。接著，Lync Server 會使用這些回應碼做出輸出路由的決定。例如，不正常的閘道可能自動被指派為「非慣用」狀態；如此一來可以將不正常閘道的使用者數量降至最少，因此可以大幅提高成功完成通話的機率。

但是，並非所有閘道都使用建議的 ISUP 原因碼，對應 Lync Server 使用的 SIP 回應碼。針對這類閘道，系統管理員可以使用 **CsSipResponseCodeTranslationRule** Cmdlet，將閘道 SIP 回應碼 (如果有 ISUP 原因碼，則二者結合) 對應到 Lync Server 使用的 SIP 回應碼。例如，閘道可能將 ISUP 原因碼 34 (「沒有可用的電路/通訊管道」) 對應到 SIP 回應碼 486 (「忙碌中」)。根據回應碼 486，Lync Server 的輸出路由邏輯不會嘗試找出新閘道以完成通話。

但是，如果是 Lync Server，該 SIP 回應碼 486 則會被對應到 SIP 回應碼 503。回應碼 503 會觸發 Lync Server 的輸出路由邏輯中的重試機制；這代表系統會試著找出另一個閘道以完成通話。為了處理這種情況，您可以建立轉譯規則，將 ISUP 原因碼 34 和 SIP 回應碼 486 的組合對應到 SIP 回應碼 503。

**Remove-CsSipResponseCodeTranslationRule** Cmdlet 提供一種方法，讓您能夠刪除先前設定為在組織中使用的任何轉譯規則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsSipResponseCodeTranslationRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsSipResponseCodeTranslationRule"}

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
<td><p>要移除的轉譯規則的唯一識別碼。轉譯規則的 Identity 由兩個部分組成：範圍 (規則設定之處) 和名稱 (建立規則時指定給它的名稱)。例如，在全域範圍建立的轉譯規則 Rule404，它的 Identity 如下：global/Rule404。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.SipResponseCodeTranslationRule\#Decorated 物件。**Remove-CsSipResponseCodeTranslationRule** Cmdlet 接受 SIP 回應碼轉譯規則物件管線傳送的執行個體。

## 傳回類型

**Remove-CsSipResponseCodeTranslationRule** Cmdlet 不會傳回任何物件或值，而是此 Cmdlet 會刪除 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.SipResponseCodeTranslationRule\#Decorated 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsSipResponseCodeTranslationRule](get-cssipresponsecodetranslationrule.md)  
[New-CsSipResponseCodeTranslationRule](new-cssipresponsecodetranslationrule.md)  
[Set-CsSipResponseCodeTranslationRule](set-cssipresponsecodetranslationrule.md)

