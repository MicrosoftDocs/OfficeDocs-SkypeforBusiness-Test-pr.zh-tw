---
title: New-CsPersistentChatAddin
TOCTitle: New-CsPersistentChatAddin
ms:assetid: 0566f4c2-0903-4dd1-87bc-784f0bdb4391
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204641(v=OCS.15)
ms:contentKeyID: 49289959
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPersistentChatAddin

 

_**上次修改主題的時間：** 2015-03-09_

可讓您設定新的常設聊天室增益集。常設聊天室增益集是自訂的網頁，可以嵌入常設聊天室用戶端。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsPersistentChatAddin -Name <String> -Url <String> [-PersistentChatPoolFqdn <String>]

## 範例

## 範例 1

範例 1 所示的命令會為 atl-cs-001.litwareinc.com 集區建立新的常設聊天室增益集 (名為 ITPersistentChatAddin)。URL 參數及 http://atl-cs-001.litwareinc.com/itchat 參數值可指定增益集網頁的位置。

    New-CsPersistentChatAddin -Name "ITPersistentChatAddin" -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com" -Url "http://atl-cs-001.litwareinc.com/itchat"

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

增益集是常設聊天室的延伸模組。增益集是和特定聊天室相關的外部應用程式 (亦即常設聊天室的內建項目)。例如「服務台」聊天室可以包含連結到網頁或 Silverlight 應用程式的 URL，以顯示當日協助要求的狀態。Lync Server 管理命令介面無法建立這些增益集，而必須使用 **CsPersistentChatAddin** Cmdlet 關聯 (或取消關聯) 聊天室的增益集。

若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPersistentChatAddin"}

**Lync Server 控制台：**若要使用 Lync Server 控制台建立新的常設聊天室增益集，請依序按一下 \[常設聊天室\]、\[增益集\] 及 \[新增\]。

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
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要為常設聊天室增益集命名的易記名稱。每個Persistent Chat Server 集區的名稱都必須是唯一的。</p></td>
</tr>
<tr class="even">
<td><p><em>Url</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>常設聊天室增益集所要顯示之網頁的 URL。</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>Persistent Chat Server 集區的完整網域名稱。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsPersistentChatAddin** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsPersistentChatAddin** Cmdlet 會建立 Microsoft.Rtc.Management.PersistentChat.Cmdlets.AddinObject 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatAddin](get-cspersistentchataddin.md)  
[Remove-CsPersistentChatAddin](remove-cspersistentchataddin.md)  
[Set-CsPersistentChatAddin](set-cspersistentchataddin.md)

