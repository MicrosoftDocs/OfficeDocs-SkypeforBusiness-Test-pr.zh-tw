---
title: Set-CsPstnUsage
TOCTitle: Set-CsPstnUsage
ms:assetid: ecba9ed6-4845-4035-933e-0c540d530b72
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399069(v=OCS.15)
ms:contentKeyID: 49292727
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPstnUsage

 

_**上次修改主題的時間：** 2015-03-09_

修改可用於識別允許之公用交換電話網路 (PSTN) 使用方式的字串集合。此 Cmdlet 可新增使用方式到 PSTN 使用方式清單，或從清單中移除使用方式。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsPstnUsage [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPstnUsage [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Usage <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此命令會將 "International" 字串新增至目前可用的 PSTN 使用方式清單。

    Set-CsPstnUsage -Identity global -Usage @{add="International"}

## 範例 2

此命令會從可用的 PSTN 使用方式清單中移除 "Local" 字串。

    Set-CsPstnUsage -Identity global -Usage @{remove="Local"}

## 範例 3

此範例的命令所執行的動作與範例 2 的命令完全相同：它會移除 "Local" PSTN 使用方式。此範例會顯示未指定 Identity 參數的命令。**Set-CsPstnUsage** Cmdlet 唯一可用的 Identity 是 Global 身分識別；省略 Identity 參數預設會使用 Global。

    Set-CsPstnUsage -Usage @{remove="Local"}

## 範例 4

此命令以 International 和 Restricted 值取代使用方式清單中的所有項目。移除先前存在的所有使用方式。

    Set-CsPstnUsage -Usage @{replace="International","Restricted"}

## 詳細描述

PSTN 使用方式是用於電話授權的字串值。PSTN 使用方式會將語音原則連結至路由。**Set-CsPstnUsage** Cmdlet 可用來在使用方式清單中新增或移除電話使用方式。此為全域清單，因此可供整個 Lync Server 部署中的原則和路由使用。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsPstnUsage** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPstnUsage"}

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
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>套用這些設定的範圍。此 Cmdlet 的 Identity 一律是 Global。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>PstnUsages</p></td>
<td><p>PSTN 使用方式物件的參照。此物件的類型必須是 PstnUsages，而且可呼叫 <strong>Get-CsPstnUsage</strong> Cmdlet 來擷取此物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>Usage</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>包含可允許的使用方式字串清單。這些項目可以是任何字串值。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnUsages 物件。接受 PSTN 使用方式物件的管線傳送資料。

## 傳回類型

此 Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnUsages 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsPstnUsage](get-cspstnusage.md)

