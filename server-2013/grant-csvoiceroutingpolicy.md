---
title: Grant-CsVoiceRoutingPolicy
TOCTitle: Grant-CsVoiceRoutingPolicy
ms:assetid: a7c7b6c4-925a-464c-a3ee-8373f4eb46b2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205141(v=OCS.15)
ms:contentKeyID: 49291926
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsVoiceRoutingPolicy

 

_**上次修改主題的時間：** 2015-03-09_

將個別使用者語音路由原則指派給一位或多位使用者。語音路由原則可管理混合語音使用者的 PSTN 使用方式。混合語音可讓 商務用 Skype Online 使用者使用 Lync Server 2013 內部部署安裝中的企業語音功能。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Grant-CsVoiceRoutingPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將個別使用者語音路由原則 RedmondVoiceRoutingPolicy 指派給 Active Directory 顯示名稱為 "Ken Myer" 的使用者。

    Grant-CsVoiceRoutingPolicy -Identity "Ken Myer" -PolicyName "RedmondVoiceRoutingPolicy"

## 範例 2

範例 2 會從使用者 Ken Myer 取消指派先前指派給該使用者的個別使用者語音路由原則；因此，Ken Myer 會由全域語音路由原則所管理。若要取消指派個別使用者原則，請將 PolicyName 設定為 Null 值 ($Null)。

    Grant-CsVoiceRoutingPolicy -Identity "Ken Myer" -PolicyName $Null

## 範例 3

範例 3 會將個別使用者語音路由原則 RedmondVoiceRoutingPolicy 指派給 Active Directory 之 Redmond OU 中的所有使用者。為達此目的，命令會先呼叫 **Get-CsUser** Cmdlet 搭配 OU 參數；參數值 "OU=Redmond,dc=litwareinc,dc=com" 可將傳回的資料限制為 Redmond OU 中的使用者帳戶。然後再將這些使用者帳戶管線傳送到 **Grant-CsVoiceRoutingPolicy** Cmdlet，以將語音路由原則 RedmondVoiceRoutingPolicy 指派給每位使用者。

    Get-CsUser -OU "OU=Redmond,dc=litwareinc,dc=com" | Grant-CsVoiceRoutingPolicy -PolicyName "RedmondVoiceRoutingPolicy"

## 詳細描述

當部分使用者位於內部部署版的 Lync Server 且其他使用者位於 商務用 Skype Online 時，就屬於「混合」狀況，可以使用語音路由原則。為您的 商務用 Skype Online 使用者指派語音路由原則，可讓這些使用者利用內部部署的 SIP 主幹撥打及接聽公用交換電話網路上的電話。

請注意，只為使用者指派語音路由原則，並無法讓使用者從 商務用 Skype Online 撥打 PSTN 電話。您還必須讓這些使用者使用企業語音，並且需要為他們指派適當的語音原則與撥號對應表。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsVoiceRoutingPolicy"}

**Lync Server 控制台：**Grant-CsVoiceRoutingPolicy Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>表示要指派個別使用者語音路由原則的使用者帳戶 Identity。通常可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主要名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (例如 Ken Myer)。</p>
<p>也可以使用使用者的 Active Directory 辨別名稱來指定使用者身分識別。</p>
<p>此外，使用顯示名稱做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會傳回所有顯示名稱結尾為字串值 &quot; Smith&quot; 的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>要指派之原則的「名稱」。簡單來說，PolicyName 是原則 Identity 減去原則範圍 (&quot;tag:&quot;首碼)。例如，Identity 為 tag:Redmond 的原則擁有與 Redmond 相等的 PolicyName；同樣地，Identity 為 tag:RedmondVoiceRoutingPolicy 的原則則擁有與 RedmondVoiceRoutingPolicy 相等的 PolicyName。</p>
<p>若要取消指派先前已指派給使用者的個別使用者原則，請將 PolicyName 設定為 Null 值 ($Null)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站擷取使用者資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-dc-001) 或其完整網域名稱 (FQDN) (例如，atl-dc-001.litwareinc.com)。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您透過代表已指派語音路由原則之使用者帳戶的管線傳遞使用者物件。根據預設， <strong>Grant-CsVoiceRoutingPolicy</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
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

字串值或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。 **Grant-CsVoiceRoutingPolicy** Cmdlet 會接受代表使用者帳戶 Identity 之字串值的管線傳送資料。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

**Grant-CsVoiceRoutingPolicy** Cmdlet 預設不會傳回值或物件。但是，如果加入 PassThru 參數，Cmdlet 就會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact 的執行個體。

## 請參閱

#### 其他資源

[Get-CsVoiceRoutingPolicy](get-csvoiceroutingpolicy.md)  
[New-CsVoiceRoutingPolicy](new-csvoiceroutingpolicy.md)  
[Remove-CsVoiceRoutingPolicy](remove-csvoiceroutingpolicy.md)  
[Set-CsVoiceRoutingPolicy](set-csvoiceroutingpolicy.md)

