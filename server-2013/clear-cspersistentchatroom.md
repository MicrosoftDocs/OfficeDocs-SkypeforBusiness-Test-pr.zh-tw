---
title: Clear-CsPersistentChatRoom
TOCTitle: Clear-CsPersistentChatRoom
ms:assetid: 6b7801d8-d924-4e97-9b17-ceb6a263a7a7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204976(v=OCS.15)
ms:contentKeyID: 49291224
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Clear-CsPersistentChatRoom

 

_**上次修改主題的時間：** 2015-03-09_

從聊天室中最舊的項目開始移除常設聊天室中的內容，一直到指定的結束日期為止。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Clear-CsPersistentChatRoom -Identity <String> <COMMON PARAMETERS>

    Clear-CsPersistentChatRoom -Instance <ChatRoom> <COMMON PARAMETERS>

    COMMON PARAMETERS: -EndDate <DateTime> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會從常設聊天室 ITChatRoom 中，移除在 2012 年 3 月 1 日當天或之前加入的所有內容。

    Clear-CsPersistentChatRoom -Identity "atl-cs-001.litwareinc.com\ITChatRoom" -EndDate "3/1/2012"

## 範例 2

範例 2 會從組織的所有聊天室中移除在 2012 年 3 月 1 日當天或之前新增的內容。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsPersistentChatRoom** Cmdlet，以傳回組織中所有聊天室的集合。然後，此集合會管線傳送到 **Clear-CsPersistentChatRoom** Cmdlet，以移除集合中每個聊天室在 2012 年 3 月 1 日當天或之前新增的內容。請注意，為了隱藏您每次嘗試清除不同聊天室時所出現的確認提示，會使用下列語法加入 Confirm 參數：

\-Confirm:$False

    Get-CsPersistentChatRoom | Clear-CsPersistentChatRoom -EndDate "3/1/2012" -Confirm:$False

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

常設聊天室的討論以在各個聊天室張貼訊息的形式進行；這些聊天室各有其討論的主題。根據設計，張貼在聊天室的訊息會永久保存，使用者可以隨時返回聊天室檢視其先前所張貼的所有訊息。

不過，系統管理員有時候可能會需要清除聊天室的所有 (或部分) 訊息，這是為了釋放一些資料庫空間，或是因為變更聊天室的主題。無論目的為何， **Clear-CsPersistentChatRoom** Cmdlet 都可讓您刪除聊天室內的所有訊息，或是刪除某段指定期間內所張貼的所有訊息 (例如所有在 2012 年 8 月 1 日前張貼的訊息)。

**注意 ：**若要針對特定目標移除其訊息 (例如特定使用者張貼的所有訊息)，請使用 [Remove-CsPersistentChatMessage](remove-cspersistentchatmessage.md) Cmdlet。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Clear-CsPersistentChatRoom"}

**Lync Server 控制台：** **Clear-CsPersistentChatRoom** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>EndDate</em></p></td>
<td><p>必要</p></td>
<td><p>System.DateTime</p></td>
<td><p>指定應移除內容的最後日期。例如，如果您指定 EndDate 為 3/1/2012 (美國英文的 2012 年 3 月 1 日)，將會刪除在 2012 年 3 月 1 日當天或之前加入聊天室的所有常設聊天室內容。</p>
<p>執行 <strong>Clear-CsPersistentChatRoom</strong> cmdlet 時，必須指定 EndDate。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>要移除其內容之聊天室的 Identity。例如：</p>
<p>-Identity &quot;atl-cs-001.litwareinc.com\ITChatRoom&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoom</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。如果您將此參數值設為 False，當您執行 Cmdlet 時，將不會出現確認提示。</p>
<p>-Confirm:$False</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Clear-CsPersistentChatRoom** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.GroupChat.Cmdlets.ChatRoomObject 物件執行個體。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Remove-CsPersistentChatMessage](remove-cspersistentchatmessage.md)

