---
title: Get-CsVoiceRoutingPolicy
TOCTitle: Get-CsVoiceRoutingPolicy
ms:assetid: 60245b7d-4e95-4925-aae5-c0fa1e9f38fc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204940(v=OCS.15)
ms:contentKeyID: 49291077
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceRoutingPolicy

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之語音路由原則的資訊。語音路由原則可管理混合語音使用者的 PSTN 使用方式。混合語音可讓位於 商務用 Skype Online 的使用者利用 Lync Server 2013 內部部署安裝中可用的企業語音功能。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsVoiceRoutingPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceRoutingPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有語音路由原則的資訊。

    Get-CsVoiceRoutingPolicy

## 範例 2

範例 2 會針對單一語音路由原則 (Identity 為 RedmondVoiceRoutingPolicy 的原則) 傳回資訊。

    Get-CsVoiceRoutingPolicy -Identity "RedmondVoiceRoutingPolicy"

## 範例 3

範例 3 所示的命令會傳回在個別使用者範圍設定之所有語音路由原則的資訊。為達此目的，命令會使用 Filter 參數搭配篩選值 "tag:\*" (此篩選值可將傳回的資料限制在 Identity 開頭為 "tag:" 字串值的原則)。

    Get-CsVoiceRoutingPolicy -Filter "tag:*"

## 範例 4

範例 4 傳回之資訊是只針對包含 PSTN 使用方式 "Long Distance" 的語音路由原則。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsVoiceRoutingPolicy** Cmdlet，以傳回設定供組織使用之所有語音路由原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 PstnUsages 屬性中包含 (-contains) 使用方式 "Long Distance" 的原則。

    Get-CsVoiceRoutingPolicy | Where-Object {$_.PstnUsages -contains "Long Distance"}

## 範例 5

範例 5 是範例 4 所示命令的變化；但此範例傳回之資訊是只針對不包含 PSTN 使用方式 "Long Distance" 的語音路由原則。為達成此目的， **Where-Object** Cmdlet 會使用 –notcontains 運算子，將傳回的資料限制為不包含使用方式 "Long Distance" 的原則。

    Get-CsVoiceRoutingPolicy | Where-Object {$_.PstnUsages -notcontains "Long Distance"}

## 詳細描述

當部分使用者位於內部部署版的 Lync Server 且其他使用者位於 商務用 Skype Online 時，就屬於「混合」狀況，可以使用語音路由原則。為您的 商務用 Skype Online 使用者指派語音路由原則，可讓這些使用者利用內部部署的 SIP 主幹撥打及接聽公用交換電話網路上的電話。

請注意，只為使用者指派語音路由原則，並無法讓使用者從 商務用 Skype Online 撥打 PSTN 電話。您還必須讓這些使用者使用企業語音，並且需要為他們指派適當的語音原則與撥號對應表。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceRoutingPolicy"}

**Lync Server 控制台：**Get-CsVoiceRoutingPolicy Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>System.Strkng</p></td>
<td><p>可讓您在擷取一或多個語音路由原則時，使用萬用字元。例如，若要傳回在個別使用者範圍設定的所有原則，請使用下列語法：</p>
<p>-Filter &quot;tag:*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要擷取之語音路由原則的唯一識別碼。若要傳回全域原則，請使用下列語法：</p>
<p>-Identity global</p>
<p>若要傳回在個別使用者範圍設定的原則，請使用下列語法：</p>
<p>-Identity &quot;RedmondVoiceRoutingPolicy&quot;</p>
<p>指定 Identity 時，您無法使用萬用字元。</p>
<p>若 Identity 和 Filter 參數皆未指定，則 <strong>Get-CsVoiceRoutingPolicy</strong> Cmdlet 會傳回設定供組織使用的所有語音路由原則。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取語音原則資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsVoiceRoutingPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsVoiceRoutingPolicy** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceRoutingPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Grant-CsVoiceRoutingPolicy](grant-csvoiceroutingpolicy.md)  
[New-CsVoiceRoutingPolicy](new-csvoiceroutingpolicy.md)  
[Remove-CsVoiceRoutingPolicy](remove-csvoiceroutingpolicy.md)  
[Set-CsVoiceRoutingPolicy](set-csvoiceroutingpolicy.md)

