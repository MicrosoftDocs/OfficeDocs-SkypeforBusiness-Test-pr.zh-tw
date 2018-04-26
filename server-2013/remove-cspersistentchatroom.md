---
title: Remove-CsPersistentChatRoom
TOCTitle: Remove-CsPersistentChatRoom
ms:assetid: 04cadd5d-13dc-4de5-b0b5-8c2f9bbbc7a7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204639(v=OCS.15)
ms:contentKeyID: 49289943
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPersistentChatRoom

 

_**上次修改主題的時間：** 2015-03-09_

移除一或多個常設聊天室。聊天室相當於討論區，通常會以特定主題為主。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsPersistentChatRoom -Identity <String> <COMMON PARAMETERS>

    Remove-CsPersistentChatRoom -Instance <ChatRoom> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除常設聊天室 RedmondChatRoom。

    Remove-CsPersistentChatRoom -Identity "atl-gc-001.litwareinc.com\RedmondChatRoom"

## 範例 2

範例 2 會移除組織所使用的所有常設聊天室。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsPersistentChatRoom** Cmdlet，以傳回所有可用聊天室的集合。然後，此集合會管線傳送到 **Remove-CsPersistentChatRoom** Cmdlet，以刪除集合中的每一個聊天室。

    Get-CsPersistentChatRoom  | Remove-CsPersistentChatRoom

## 範例 3

範例 3 會移除所有「已關閉」的聊天室 (已關閉的聊天室表示表示任何使用者只要進行目錄搜查，就可以找到該聊天室，但只有成員才可參加聊天室活動)。為了完成此工作，命令會先使用 **Get-CsPersistentChatRoom** Cmdlet 和 Privacy 參數傳回所有已關閉之聊天室的集合。然後，此集合會管線傳送到 **Remove-CsPersistentChatConfiguration** Cmdlet，以刪除集合中的每個聊天室。

    Get-CsPersistentChatRoom -Privacy "Closed"  | Remove-CsPersistentChatRoom

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

常設聊天室的討論以在各個聊天室張貼訊息的形式進行；這些聊天室各有其討論的主題。根據設計，張貼在聊天室的訊息會永久保存，使用者可以隨時返回聊天室檢視其先前所張貼的所有訊息。

**Remove-CsPersistentChatRoom** Cmdlet 可讓系統管理員移除一或多個設定供組織使用的常設聊天室。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示中執行下列命令

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPersistentChatRoom"}

**Lync Server 控制台：**若要使用 Lync Server 控制台 刪除現有的常設聊天室，請按一下 \[常設聊天室\]，再按一下 \[聊天室\]，然後選取要刪除的聊天室。若要刪除聊天室，請按一下 \[編輯\]，然後按一下 \[刪除\]。

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
<td><p>System.Strkng</p></td>
<td><p>要移除之常設聊天室的唯一識別碼。聊天室的 Identity 由包含經過設定並已加上名稱之聊天室的常設聊天室集區組成：例如：</p>
<p>-Identity &quot;atl-gc-001.litwareinc.com\RedmondChatRoom&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoom</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Remove-CsPersistentChatRooms** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.PersistentChat.Cmdlets.ChatRoomObject 物件執行個體。

## 傳回類型

無。反之， **Remove-CsPersistentChatRoom** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.PersistentChat.Cmdlets.ChatRoomObject 物件執行個體。

## 請參閱

#### 其他資源

[Clear-CsPersistentChatRoom](clear-cspersistentchatroom.md)  
[Get-CsPersistentChatRoom](get-cspersistentchatroom.md)  
[New-CsPersistentChatRoom](new-cspersistentchatroom.md)  
[Set-CsPersistentChatRoom](set-cspersistentchatroom.md)

