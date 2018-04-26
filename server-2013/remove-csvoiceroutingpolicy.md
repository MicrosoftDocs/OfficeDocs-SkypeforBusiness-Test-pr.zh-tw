---
title: Remove-CsVoiceRoutingPolicy
TOCTitle: Remove-CsVoiceRoutingPolicy
ms:assetid: 3729e908-5c0d-4970-bdff-5869ba2082c9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204799(v=OCS.15)
ms:contentKeyID: 49290579
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsVoiceRoutingPolicy

 

_**上次修改主題的時間：** 2015-03-09_

刪除現有的語音路由原則。語音路由原則可管理混合語音使用者的 PSTN 使用方式。混合語音可讓 商務用 Skype Online 使用者使用 Lync Server 2013 內部部署安裝中的企業語音功能。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsVoiceRoutingPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除語音路由原則 RedmondVoiceRoutingPolicy

    Remove-CsVoiceRoutingPolicy -Identity "RedmondVoiceRoutingPolicy"

## 範例 2

在範例 2 中，會移除在個別使用者範圍設定的所有語音路由原則。為達成此目的，命令會先呼叫 **Get-CsVoiceRoutingPolicy** Cmdlet 搭配 Filter 參數；篩選值 "tag:\*" 可將傳回的資料限制在個別使用者範圍所設定的語音路由原則。然後再將這些個別使用者原則管線傳送到 **Remove-CsVoiceRoutingPolicy** Cmdlet 加以刪除。

    Get-CsVoiceRoutingPolicy -Filter "tag:*" | Remove-CsVoiceRoutingPolicy

## 範例 3

在範例 3 中，會移除包含 PSTN 使用方式 "Long Distance" 的所有語音路由原則。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsVoiceRoutingPolicy** Cmdlet，以傳回所有可用語音路由原則的集合。然後，此集合會管線傳送到 Where-Object Cmdlet，這會只挑出 PstnUsages 屬性中包含 (-contains) 使用方式 "Long Distance" 的原則。接著將符合該準則的原則管線傳送到 **Remove-CsVoiceRoutingPolicy**，以移除包含 PSTN 使用方式 "Long Distance" 的每個語音路由原則。

    Get-CsVoiceRoutingPolicy | Where-Object {$_.PstnUsages -contains "Long Distance"} | Remove-CsVoiceRoutingPolicy

## 詳細描述

當部分使用者位於內部部署版的 Microsoft Lync Server 2013 且其他使用者位於 商務用 Skype Online 時，就屬於「混合」狀況，可以使用語音路由原則。為您的 商務用 Skype Online 使用者指派語音路由原則，可讓這些使用者利用內部部署的 SIP 主幹撥打及接聽公用交換電話網路上的電話。

請注意，只為使用者指派語音路由原則，並無法讓使用者從 商務用 Skype Online 撥打 PSTN 電話。您還必須讓這些使用者使用企業語音，並且需要為他們指派適當的語音原則與撥號對應表。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsVoiceRoutingPolicy"}

**Lync Server 控制台：** **Remove-CsVoiceRoutingPolicy** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>要移除之語音路由原則的唯一識別碼。若要「移除」全域原則，請使用下列語法：</p>
<p>-Identity global</p>
<p>請注意，此參數實際上不會移除全域原則，而是將該原則中的所有屬性重設為其預設值。</p>
<p>若要移除個別使用者原則，請使用類似下列的語法：</p>
<p>-Identity &quot;RedmondVoiceRoutingPolicy&quot;</p>
<p>在指定原則 Identity 時不能使用萬用字元。</p></td>
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
<td><p>若此參數已存在，即使原則目前已指派給至少一位使用者，也將會自動移除。</p>
<p>若此參數不存在，則 <strong>Remove-CsVoiceRoutingPolicy</strong> Cmdlet 就不會自動移除已指派給至少一位使用者的個別使用者原則。但是會顯示確認提示，詢問您是否確定要移除該原則。您必須回答是 (按下 Y 鍵)，命令才會繼續並移除該原則。</p></td>
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

**Remove-CsVoiceRoutingPolicy** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceRoutingPolicy 物件執行個體。

## 傳回類型

無。反之，**Remove-CsVoiceRoutingPolicy** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceRoutingPolicy 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsVoiceRoutingPolicy](get-csvoiceroutingpolicy.md)  
[Grant-CsVoiceRoutingPolicy](grant-csvoiceroutingpolicy.md)  
[New-CsVoiceRoutingPolicy](new-csvoiceroutingpolicy.md)  
[Set-CsVoiceRoutingPolicy](set-csvoiceroutingpolicy.md)

