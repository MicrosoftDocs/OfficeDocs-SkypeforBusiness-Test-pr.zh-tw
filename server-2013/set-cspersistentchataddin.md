---
title: Set-CsPersistentChatAddin
TOCTitle: Set-CsPersistentChatAddin
ms:assetid: 1badd6b5-e519-47a1-9434-9fa5a00b79ff
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204721(v=OCS.15)
ms:contentKeyID: 49290258
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatAddin

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的常設聊天室增益集。常設聊天室增益集是自訂的網頁，可以嵌入常設聊天室用戶端中。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsPersistentChatAddin -Instance <Addin> <COMMON PARAMETERS>

    Set-CsPersistentChatAddin -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Name <String>] [-Url <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會修改指派給 ITPersistentChatAddin 常設聊天室增益集的 URL。在此情況下，URL 會變更為 http://atl-cs-001.litwareinc.com/itchat2。

    Set-CsPersistentChatAddin -Identity "atl-cs-001.litwareinc.com\ITPersistentChatAddin" -Url "http://atl-cs-001.litwareinc.com/itchat2"

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

增益集是常設聊天室的延伸模組。增益集是和特定聊天室相關的外部應用程式 (亦即，不是常設聊天室的內建項目)。例如，服務台聊天室可以包含連結到網頁或 Silverlight 應用程式的 URL，以顯示當日協助要求的狀態。 Lync ServerWindows PowerShell 命令列介面 Cmdlet 未提供建立這些增益集的功能，而是使用 **CsPersistentChatAddin** Cmdlet，從聊天室關聯 (或取消關聯) 增益集。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatAddin"}

**Lync Server 控制台：**若要使用 Lync Server 控制台 修改現有的常設聊天室增益集，請依序按一下 **\[常設聊天室\]** 及 **\[增益集\]**，然後按兩下所要修改的增益集。

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
<td><p>常設聊天室增益集的唯一識別碼。Identity 的組成包括增益集所在之常設聊天室集區的完整網域名稱、&quot;\&quot; 字元及增益集名稱。例如：</p>
<p>-Identity &quot;atl-gc-001.litwareincom\ITPersistentChatAddin&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.Addin</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>為常設聊天室增益集命名的易記名稱。每個常設聊天室集區的名稱都必須是唯一的。</p></td>
</tr>
<tr class="odd">
<td><p><em>Url</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>常設聊天室增益集所要顯示之網頁的 URL。</p></td>
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

**Set-CsPersistentChatAddin** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.PersistentChat.Cmdlets.AddinObject 物件執行個體。

## 傳回類型

無。反之， **Set-CsPersistentChatAddin** Cmdlet 會修改現有的 Microsoft.Rtc.Management.PersistentChat.Cmdlets.AddinObject 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatAddin](get-cspersistentchataddin.md)  
[New-CsPersistentChatAddin](new-cspersistentchataddin.md)  
[Remove-CsPersistentChatAddin](remove-cspersistentchataddin.md)

