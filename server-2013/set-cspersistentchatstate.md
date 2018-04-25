---
title: Set-CsPersistentChatState
TOCTitle: Set-CsPersistentChatState
ms:assetid: 9b82fe41-214d-4376-b026-bb1434d04118
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205109(v=OCS.15)
ms:contentKeyID: 49291787
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatState

 

_**上次修改主題的時間：** 2015-03-09_

修改常設聊天室服務集區的狀態。常設聊天室集區可以是下列兩種狀態之一：Normal (表示集區可以正常運作，並可接受新的用戶端連線) 或 FailedOver (表示集區無法接受用戶端連線)。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsPersistentChatState [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPersistentChatState [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-PoolState <FailedOver | Normal>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將 Persistent Chat Server atl-gc-001.litwareinc.com 的集區狀態設為 FailedOver。

    Set-CsPersistentChatState -Identity "PersistentChatServer:atl-gc-001.litwareinc.com" -PoolState "FailedOver"

## 詳細描述

[Get-CsPersistentChatState](get-cspersistentchatstate.md) Cmdlet 會傳回一或多個常設聊天室集區的狀態。常設聊天室集區可以是下列兩種狀態之一：Normal (表示集區使用的是主要資料庫) 或 FailedOver (表示集區使用的是備份資料庫)。您可以使用 **Set-CsPersistentChatState** Cmdlet 變更常設聊天室集區的狀態。當您變更集區的狀態時， Lync Server 2013 會自動變更集區中每部伺服器的狀態。若要變更個別聊天伺服器的狀態，請使用 [Set-CsPersistentChatActiveServer](set-cspersistentchatactiveserver.md) Cmdlet。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatState"}

**Lync Server 控制台：** **Set-CsPersistentChatState** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>套用新服務狀態之常設聊天室集區的服務識別。例如：</p>
<p>-Identity PersistentChatServer:atl-persistentchat-001.litwareinc.com</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolState</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PoolState</p></td>
<td><p>常設聊天室集區的目前狀態。有效值為：</p>
<p>* Normal</p>
<p>* FailedOver</p>
<p>預設值為 Normal。</p></td>
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

**Set-CsPersistentChatState** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatState 物件執行個體。

## 傳回類型

無。反之， **Set-CsPersistentChatState** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatState 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatState](get-cspersistentchatstate.md)  
[Set-CsPersistentChatActiveServer](set-cspersistentchatactiveserver.md)

