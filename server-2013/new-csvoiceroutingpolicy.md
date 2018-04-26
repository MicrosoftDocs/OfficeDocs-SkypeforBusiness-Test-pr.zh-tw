---
title: New-CsVoiceRoutingPolicy
TOCTitle: New-CsVoiceRoutingPolicy
ms:assetid: 9e5bd6f6-902f-4911-ab88-9abb581df7fd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205135(v=OCS.15)
ms:contentKeyID: 49291839
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoiceRoutingPolicy

 

_**上次修改主題的時間：** 2015-03-09_

建立新的語音路由原則。語音路由原則可管理混合語音使用者的 PSTN 使用方式。混合語音可讓位於 商務用 Skype Online 的使用者利用 Lync Server 2013 內部部署安裝中提供的企業語音功能。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsVoiceRoutingPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Name <String>] [-PstnUsages <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立其 Identity 為 RedmondVoiceRoutingPolicy 的新個別使用者語音路由原則，並將單一 PSTN 使用方式 Long Distance 指派給此原則。

    New-CsVoiceRoutingPolicy -Identity "RedmondVoiceRoutingPolicy" -Name "RedmondVoiceRoutingPolicy" -PstnUsages "Long Distance"

## 範例 2

範例 2 是範例 1 所示命令的另一種變化；但此範例會指派下列三個 PSTN 使用方式給新原則：Long Distance、Local 及 Internal。只要使用逗號分隔每個使用方式，即可指派多個使用方式。

    New-CsVoiceRoutingPolicy -Identity "RedmondVoiceRoutingPolicy" -Name "RedmondVoiceRoutingPolicy" -PstnUsages "Long Distance", "Local", "Internal"

## 詳細描述

當部分使用者位於內部部署版的 Lync Server 且其他使用者位於 商務用 Skype Online 時，就屬於「混合」狀況，可以使用語音路由原則。為您的 商務用 Skype Online 使用者指派語音路由原則，可讓這些使用者利用內部部署的 SIP 主幹撥打及接聽公用交換電話網路上的電話。

請注意，只為使用者指派語音路由原則，並無法讓使用者從 商務用 Skype Online 撥打 PSTN 電話。您還必須讓這些使用者使用企業語音，並且需要為他們指派適當的語音原則與撥號對應表。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoiceRoutingPolicy"}

**Lync Server 控制台：**New-CsVoiceRoutingPolicy Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>指派給新語音路由原則的唯一識別碼。由於您只能在個別使用者範圍建立新原則，因此，Identity 一律是指派給原則的「名稱」。例如：</p>
<p>-Identity &quot;RedmondVoiceRoutingPolicy&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓系統管理員提供語音路由原則隨附的說明文字。例如，Description 可包含被指派原則的使用者相關資訊。</p></td>
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

無。 **New-CsVoiceRoutingPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsVoiceRoutingPolicy** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceRoutingPolicy 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsVoiceRoutingPolicy](get-csvoiceroutingpolicy.md)  
[Grant-CsVoiceRoutingPolicy](grant-csvoiceroutingpolicy.md)  
[Remove-CsVoiceRoutingPolicy](remove-csvoiceroutingpolicy.md)  
[Set-CsVoiceRoutingPolicy](set-csvoiceroutingpolicy.md)

