---
title: Set-CsVoiceRoutingPolicy
TOCTitle: Set-CsVoiceRoutingPolicy
ms:assetid: cff51726-88c6-4cdf-aaad-a7246c4408c5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205313(v=OCS.15)
ms:contentKeyID: 49292374
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceRoutingPolicy

 

_**上次修改主題的時間：** 2015-05-28_

修改現有的語音路由原則。語音路由原則可管理混合語音使用者的 PSTN 使用方式。混合語音可讓 商務用 Skype Online 使用者使用 Lync Server 2013 內部部署安裝中的企業語音功能。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsVoiceRoutingPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceRoutingPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-Name <String>] [-PstnUsages <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將 PSTN 使用方式 "Long Distance" 新增至個別使用者語音路由原則 RedmondVoiceRoutingPolicy。

    Set-CsVoiceRoutingPolicy -Identity "RedmondVoiceRoutingPolicy" -PstnUsages @{Add="Long Distance"}

## 範例 2

範例 2 會從個別使用者語音路由原則 RedmondVoiceRoutingPolicy 移除 PSTN 使用方式 "Local"。

    Set-CsVoiceRoutingPolicy -Identity "RedmondVoiceRoutingPolicy" -PstnUsages @{Remove="Local"}

## 範例 3

範例 3 會從包含 PSTN 使用方式 "Local" 的所有語音路由原則移除該使用方式。為達成此目的，命令會呼叫不含任何參數的 **Get-CsVoiceRoutingPolicy** Cmdlet，以傳回所有可用語音路由原則的集合。然後，此集合會管線傳送到 Where-Object Cmdlet，這會只挑出 PstnUsages 屬性包含 (-contains) "Local" 使用方式的原則。接著將這些原則管線傳送到 **Set-CsVoiceRoutingPolicy** Cmdlet，以從每個原則刪除 Local 使用方式。

    Get-CsVoiceRoutingPolicy | Where-Object {$_.PstnUsages -contains "Local"} | Set-CsVoiceRoutingPolicy -PstnUsages @{Remove="Local"}

## 詳細描述

當部分使用者位於內部部署版的 Lync Server 且其他使用者位於 商務用 Skype Online 時，就屬於「混合」狀況，可以使用語音路由原則。為您的 商務用 Skype Online 使用者指派語音路由原則，可讓這些使用者利用內部部署的 SIP 主幹撥打及接聽公用交換電話網路上的電話。

請注意，只為使用者指派語音路由原則，並無法讓使用者從 商務用 Skype Online 撥打 PSTN 電話。您還必須讓這些使用者使用企業語音，並且需要為他們指派適當的語音原則與撥號對應表。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceRoutingPolicy"}

**Lync Server 控制台：**Set-CsVoiceRoutingPolicy Cmdlet 的執行功能並未提供於　Lync Server 控制台。

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
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓系統管理員提供語音路由原則隨附的說明文字。例如，Description 可包含被指派原則的使用者相關資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>建立原則時指派給原則的唯一識別碼。語音路由原則可以在全域範圍或個別使用者範圍指派。若要參考全域執行個體，請使用下列語法：</p>
<p>-Identity global</p>
<p>若要參考個別使用者原則，請使用類似下列的語法：</p>
<p>-Identity &quot;RedmondVoiceRoutingPolicy&quot;</p>
<p>若未指定 Identity，則 <strong>Set-CsVoiceRoutingPolicy</strong> Cmdlet 將會修改全域原則。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>描述此原則的易記名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnUsages</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>可套用至此語音路由原則的 PSTN 使用方式 (例如 Local 或 Long Distance) 清單。PSTN 使用方式必須是現有的使用方式(您可以呼叫 <strong>Get-CsPstnUsage</strong> Cmdlet 來擷取 PSTN使用方式)。</p></td>
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

**Set-CsVoiceRoutingPolicy** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceRoutingPolicy 物件執行個體。

## 傳回類型

無。反之， **Set-CsVoiceRoutingPolicy** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceRoutingPolicy 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsVoiceRoutingPolicy](get-csvoiceroutingpolicy.md)  
[Grant-CsVoiceRoutingPolicy](grant-csvoiceroutingpolicy.md)  
[New-CsVoiceRoutingPolicy](new-csvoiceroutingpolicy.md)  
[Remove-CsVoiceRoutingPolicy](remove-csvoiceroutingpolicy.md)

