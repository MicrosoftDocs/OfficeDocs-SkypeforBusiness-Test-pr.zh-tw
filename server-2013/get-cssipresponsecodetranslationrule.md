---
title: Get-CsSipResponseCodeTranslationRule
TOCTitle: Get-CsSipResponseCodeTranslationRule
ms:assetid: 075e9e85-8f85-402c-9256-4e73ec93f96b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398130(v=OCS.15)
ms:contentKeyID: 49289986
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsSipResponseCodeTranslationRule

 

_**上次修改主題的時間：** 2015-03-09_

傳回 SIP 回應碼轉譯規則的資訊。這些規則可讓系統管理員將介於 400 到 699 的 SIP 回應碼值對應到 Lync Server 使用的值。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsSipResponseCodeTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsSipResponseCodeTranslationRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有回應碼轉譯規則的集合。若要執行此作業，可呼叫不含任何參數的 **Get-CsSipResponseCodeTranslationRule** Cmdlet。

    Get-CsSipResponseCodeTranslationRule

## 範例 2

範例 2 會傳回單一回應碼轉譯規則：Identity 為 PstnGateway:192.168.0.240/Rule404 的規則。

    Get-CsSipResponseCodeTranslationRule -Identity "PstnGateway:192.168.0.240/Rule404"

## 範例 3

在範例 3 中，Filter 參數用來將傳回的資料限制為在網站範圍設定的所有回應碼轉譯規則。篩選值 "site:\*" 會將傳回的資料限制為 Identity 開頭為字串值 "site:" 的規則。

    Get-CsSipResponseCodeTranslationRule -Filter "site:*"

## 範例 4

範例 4 所示的命令會傳回尚未針對 ReceivedISUPCauseValue 屬性設定任何值之所有回應碼轉譯規則的集合。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsSipResponseCodeTranslationRule** Cmdlet，以傳回目前使用之所有回應碼轉譯規則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 ReceivedISUPCauseValue 屬性等於 -1 的規則。

    Get-CsSipResponseCodeTranslationRule | Where-Object {$_.ReceivedISUPCauseValue -eq -1}

## 詳細描述

SIP 主幹連線可用於連接 Voice over Internet Protocol (VoIP) 網路 (例如 Enterprise Voice) 與公用交換電話網路 (PSTN)。在 Lync Server 中，中繼伺服器 使用對等主幹與 PSTN 網路互動。PSTN 網路上的撥出電話無法作用時，系統會自動產生 ISDN User Part (ISUP) 原因碼。例如，PSTN 閘道可能傳送原因碼 34，代表沒有可用的電路或通訊管道可以完成通話。中繼伺服器 對等主幹收到該 ISUP 原因碼時，會將原因碼轉換為 SIP 回應碼，並且將這個回應碼傳送給 中繼伺服器 本身。接著，Lync Server 會使用這些回應碼做出輸出路由的決定。例如，不正常的閘道可能自動被指派為「非慣用」狀態；如此一來可以將不正常閘道的使用數量降至最少，因此可以大幅提高成功完成通話的機率。

但是，並非所有閘道都使用建議的 ISUP 原因碼，對應 Lync Server 使用的 SIP 回應碼。針對這類閘道，系統管理員可以使用 **CsSipResponseCodeTranslationRule** Cmdlet，將閘道 SIP 回應碼 (如果有 ISUP 原因碼，則二者結合) 對應到 Lync Server 使用的 SIP 回應碼。例如，閘道可能將 ISUP 原因碼 34 (「沒有可用的電路/通訊管道」) 對應到 SIP 回應碼 486 (「忙碌中」)。根據回應碼 486，Lync Server 的輸出路由邏輯不會嘗試找出新閘道以完成通話。

但是，如果是 Lync Server，該 SIP 回應碼 486 則會被對應到 SIP 回應碼 503。回應碼 503 會觸發 Lync Server 的輸出路由邏輯中的重試機制；這代表系統會試著找出另一個閘道以完成通話。為了處理這種情況，您可以建立轉譯規則，將 ISUP 原因碼 34 和 SIP 回應碼 486 的組合對應到 SIP 回應碼 503。

**Get-CsSipResponseCodeTranslationRule** Cmdlet 可讓您擷取設定為在組織中使用之所有轉譯規則的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsSipResponseCodeTranslationRule** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsSipResponseCodeTranslationRule"}

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
<td><p>可讓您在指定要傳回的轉譯規則 (或多個規則) 時使用萬用字元。例如，下列語法會傳回其 Identity 中的字串值為 &quot;404&quot; 的所有轉譯規則：</p>
<p>-Filter &quot;*404*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>轉譯規則的唯一識別碼。轉譯規則的 Identity 包含兩個部分：設定規則的範圍，以及建立規則時指定的規則名稱。例如，在全域範圍建立，且名稱為 Rule404 之轉譯規則的 Identity 會類似如下：global/Rule404。</p>
<p>除了全域範圍之外，也可以在網站範圍或服務範圍建立轉譯規則 (儘管只針對 PstnGateway 服務)。</p>
<p>若要傳回針對特定網站或服務建立的所有轉譯規則，您只要指定網站或服務 Identity 即可。例如：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>如果省略此參數，<strong>Get-CsSipResponseCodeTranslationRule</strong> Cmdlet 會傳回所有 SIP 回應碼轉譯規則的集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取 SIP 回應碼轉譯規則資料，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsSipResponseCodeTranslationRule** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsSipResponseCodeTranslationRule** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.SipResponseCodeTRanslationRule\#Decorated 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsSipResponseCodeTranslationRule](new-cssipresponsecodetranslationrule.md)  
[Remove-CsSipResponseCodeTranslationRule](remove-cssipresponsecodetranslationrule.md)  
[Set-CsSipResponseCodeTranslationRule](set-cssipresponsecodetranslationrule.md)

