---
title: Get-CsPersistentChatState
TOCTitle: Get-CsPersistentChatState
ms:assetid: 598086c9-a8c7-4b81-84ba-1807f1183024
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204915(v=OCS.15)
ms:contentKeyID: 49291007
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatState

 

_**上次修改主題的時間：** 2015-03-09_

傳回一或多個常設聊天室服務集區的狀態。常設聊天室集區可以是下列兩種狀態之一：Normal (表示集區可以正常運作，並可接受新的用戶端連線) 或 FailedOver (表示集區無法接受用戶端連線)。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsPersistentChatState [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPersistentChatState [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有 Persistent Chat Server 的狀態。

    Get-CsPersistentChatState

## 範例 2

    Get-CsPersistentChatState -Identity "PersistentChatServer:atl-gc-001.litwareinc.com"

## 範例 3

範例 3 會傳回 litwareinc.com 網域中所有 Persistent Chat Server 的狀態資訊。為達成此目的，命令會加入 Filter 參數並使用篩選值 "\*.litwareinc.com"。此篩選值會使 **Get-CsPersistentChatState** Cmdlet 傳回 Identity 結尾為字串值 ".litwareinc.com" 之所有 Persistent Chat Server 的資訊。

    Get-CsPersistentChatState -Filter "*.litwareinc.com"

## 範例 4

範例 4 所示的命令會傳回目前已容錯移轉之所有 Persistent Chat Server 的狀態資訊。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsPersistentChatState** Cmdlet，以傳回組織中所有 Persistent Chat Server 的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 PoolState 屬性等於 (-eq) "FailedOver" 的伺服器。

    Get-CsPersistentChatState | Where-Object {$_.PoolState -eq "FailedOver"}

## 詳細描述

**Get-CsPersistentChatState** Cmdlet 會傳回一或多個常設聊天室集區的狀態。常設聊天室集區可以是下列兩種狀態之一：Normal (表示集區使用的是主要資料庫) 或 FailedOver (表示集區使用的是備份資料庫)。您可以使用 [Set-CsPersistentChatState](set-cspersistentchatstate.md) Cmdlet 變更常設聊天室集區的狀態。當您變更集區的狀態時， Lync Server 2013 會自動變更集區中每部伺服器的狀態。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatState"}

**Lync Server 控制台：** **Get-CsPersistentChatState** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>可讓您在擷取一或多個常設聊天室狀態時，使用萬用字元。例如，若要傳回 litwareinc.com 網域的所有常設聊天室狀態，請使用下列語法：</p>
<p>-Filter &quot;*.litwareinc.com&quot;</p>
<p>請勿在同一個命令中同時使用 Filter 參數和 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>常設聊天室集區的唯一識別碼。例如：</p>
<p>–Identity &quot;PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p>
<p>如果省略此參數， <strong>Get-CsPersistentChatState</strong> Cmdlet 就會傳回所有常設聊天室狀態的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取常設聊天室狀態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsPersistentChatState** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPersistentChatState** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatState 物件的執行個體。

## 請參閱

#### 其他資源

[Set-CsPersistentChatState](set-cspersistentchatstate.md)

