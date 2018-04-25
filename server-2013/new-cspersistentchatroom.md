---
title: New-CsPersistentChatRoom
TOCTitle: New-CsPersistentChatRoom
ms:assetid: b00d353b-5b5b-40d6-b952-3c35170fbf8a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205166(v=OCS.15)
ms:contentKeyID: 49292005
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPersistentChatRoom

 

_**上次修改主題的時間：** 2015-03-09_

建立新的常設聊天室。聊天室相當於討論區，通常會以特定主題為主。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsPersistentChatRoom -Category <String> -Name <String> [-Addin <String>] [-Description <String>] [-Disabled <$true | $false>] [-Invitations <False | Inherit>] [-PersistentChatPoolFqdn <String>] [-Privacy <Open | Closed | Secret>] [-Type <Normal | Auditorium>]

## 範例

## 範例 1

範例 1 所示的命令會在集區 atl-cs-001.litwareinc.com 上建立名為 ITChatRoom 的新常設聊天室。此範例會將聊天室新增至 IT 類別。

    New-CsPersistentChatRoom -Name "ITChatRoom" -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com"-Category "IT"

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

常設聊天室的討論以在各個聊天室張貼訊息的形式進行；這些聊天室各有其討論的主題。根據設計，張貼在聊天室的訊息會永久保存，使用者可以隨時返回聊天室檢視其先前所張貼的所有訊息。

**New-CsPersistentChatRoom** Cmdlet 可讓系統管理員建立新的常設聊天室。請注意，使用 **New-CsPersistentChatRoom** Cmdlet 時並無法使用所有的聊天室屬性。例如，此 Cmdlet 無法用於指派聊天室管理員或簡報者。若要指派管理員或簡報者，必須先建立聊天室，然後再使用 [Set-CsPersistentChatRoom](set-cspersistentchatroom.md) Cmdlet 進行指派。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPersistentChatRoom"}

**Lync Server 控制台：**若要使用 Lync Server 控制台 建立新的常設聊天室，請依序按一下 **\[常設聊天室\]**、**\[聊天室\]**，以及 **\[新增\]**。

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
<td><p><em>Category</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>要建立聊天室的類別，例如：</p>
<p>-Category &quot;IT&quot;</p>
<p>請注意，指定的類別必須已存在，否則命令會失敗。類別是常設聊天室的集合，可以使用 <strong>New-CsPersistentChatCategory</strong> Cmdlet 來建立。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>新的常設聊天室名稱。每個常設聊天室集區的名稱都必須是唯一的。</p></td>
</tr>
<tr class="odd">
<td><p><em>Addin</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>常設聊天室增益集的名稱。如已指定，則會與聊天室相關聯。常設聊天室增益集是可在常設聊天室用戶端內嵌的自訂網頁。這些增益集可以使用 <strong>New-CsPersistentChatAddin</strong> Cmdlet 來建立。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓系統管理員提供新聊天室的其他資訊</p></td>
</tr>
<tr class="odd">
<td><p><em>Disabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如有指定此參數，會在第一次建立新聊天室時予以停用，因此無法使用。如果未使用此參數，則會啟用新聊天室，以立即使用。</p></td>
</tr>
<tr class="even">
<td><p><em>Invitations</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomInvitations</p></td>
<td><p>指定是否要繼承類別的對於新聊天室的邀請。這表示 AllowedMembers 清單上的使用者會在新聊天室建立之後，自動收到加入新聊天室的邀請。</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>新聊天室所在之常設聊天室集區的完整網域名稱。例如：</p>
<p>-PersistentChatPoolFqdn &quot;atl-gc-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Privacy</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomPrivacy</p></td>
<td><p>新聊天室的隱私權設定。允許的值為：</p>
<p>* Open (所有使用者都可以執行目錄搜尋來尋找聊天室，且所有人都可以參與聊天室活動)</p>
<p>* Secret (只有聊天室成員可以執行目錄搜尋來尋找聊天室，且只有成員可以參與聊天室活動)</p>
<p>* Closed (所有使用者都可以執行目錄搜尋來尋找聊天室，但是只有成員可以參與聊天室活動)</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomType</p></td>
<td><p>指定是否應該將新聊天室設定為 Normal (所有成員都可以張貼訊息) 或 Auditorium (只有簡報者可以張貼訊息)。例如：</p>
<p>-Type &quot;Auditorium&quot;</p>
<p>預設值為 Normal。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **New-CsPersistentChatRoom** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsPersistentChatRoom** Cmdlet 會建立 Microsoft.Rtc.Management.PersistentChat.Cmdlets.ChatRoomObject 物件的新執行個體。

## 請參閱

#### 其他資源

[Clear-CsPersistentChatRoom](clear-cspersistentchatroom.md)  
[Get-CsPersistentChatRoom](get-cspersistentchatroom.md)  
[Remove-CsPersistentChatRoom](remove-cspersistentchatroom.md)  
[Set-CsPersistentChatRoom](set-cspersistentchatroom.md)

