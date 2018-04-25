---
title: Set-CsPersistentChatActiveServer
TOCTitle: Set-CsPersistentChatActiveServer
ms:assetid: 88c0af42-cb47-4c34-bf54-9c134dcbb843
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205065(v=OCS.15)
ms:contentKeyID: 49291573
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatActiveServer

 

_**上次修改主題的時間：** 2013-03-07_

管理作用中之 Persistent Chat Server 的清單。作用中伺服器是指正常運作，並可接受新用戶端連線的 Persistent Chat Server (在指定的常設聊天室服務集區中)。集區中未標示為作用中伺服器的伺服器表示其或為正常運作，但目前無法接受新的用戶端連線。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsPersistentChatActiveServer -ActiveServers <PSListModifier> <COMMON PARAMETERS>

    Set-CsPersistentChatActiveServer -Swap <SwitchParameter> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Identity <XdsGlobalRelativeIdentity>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將 atl-gc-001.litwareinc.com 伺服器新增至作用中 Persistent Chat Server 的集合。

    Set-CsPersistentChatActiveServer -Identity "global" -ActiveServers @{Add="atl-gc-001.litwareinc.com"}

## 範例 2

範例 2 會從作用中 Persistent Chat Server 的集合移除 atl-gc-001.litwareinc.com 伺服器。

    Set-CsPersistentChatActiveServer -Identity "global" -ActiveServers @{Remove="atl-gc-001.litwareinc.com"}

## 範例 3

範例 3 所示的命令會移除所有作用中 Persistent Chat Server。移除所有作用中伺服器的作業通常會在容錯回復或容錯移轉案例中進行。

    Set-CsPersistentChatActiveServer -Identity "global" -ActiveServers $Null

## 詳細描述

**Set-CsPersistentChatActiveServer** Cmdlet 可讓系統管理員實地啟用或停用常設聊天室集區中一或多部伺服器上的常設聊天室服務。列在作用中伺服器清單上的伺服器將可以接受新的用戶端連線，反之則無法接受新的用戶端連線 (但伺服器仍會繼續在將其從清單上移除之前就進行的用戶端連線)。若要啟用 Persistent Chat Server 上的常設聊天室服務，請將該伺服器新增到作用中伺服器清單。若要停用該服務，只要從作用中伺服器清單中移除該伺服器即可。

若要啟用/停用集區中所有伺服器的常設聊天室服務，請使用 **Set-CsPersistentChatState** Cmdlet。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatActiveServer"}

**Lync Server 控制台：** **Set-CsPersistentChatActiveServer** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>ActiveServers</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>代表作用中 Persistent Chat Server 之完整網域名稱的集合。</p></td>
</tr>
<tr class="even">
<td><p><em>Swap</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，將會切換指定集區中所有 Persistent Chat Server 的作用中狀態，亦即將作用中伺服器標記為非作用中，將非作用中的伺服器標記為作用中。</p></td>
</tr>
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
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>作用中伺服器集合的唯一 Identity。請注意，您只能有單一、全域的 Persistent Chat Server 的集合。</p></td>
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

無。 **Set-CsPersistentChatActiveServer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Set-CsPersistentChatState](set-cspersistentchatstate.md)

