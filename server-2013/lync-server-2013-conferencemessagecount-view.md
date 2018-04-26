---
title: ConferenceMessageCount 檢視
TOCTitle: ConferenceMessageCount 檢視
ms:assetid: 8ee3ee95-fb78-4d4e-bcdd-6ce5a0a23b44
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688129(v=OCS.15)
ms:contentKeyID: 49890202
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ConferenceMessageCount 檢視

 

_**上次修改主題的時間：** 2015-03-09_

ConferenceMessageCount 檢視會儲存關於使用者傳送多少則訊息到會議的資訊。此檢視已於 Microsoft Lync Server 2013 引進使用。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ConferenceMessageCount 檢視包含 <a href="lync-server-2013-conferencesessiondetails-view.md">ConferenceSessionDetails 檢視</a>中的所有欄以及下方所列的欄。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>資料類型</th>
<th>詳細資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>UserUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>傳送訊息之使用者的 URI。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>傳送訊息之使用者的 URI 類型。如需詳細資訊，請參閱 <a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserTenant</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>傳送訊息之使用者的租用戶。如需詳細資訊，請參閱＜<a href="lync-server-2013-tenants-table.md">Lync Server 2013 中的 Tenants 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserMessageCount</strong></p></td>
<td><p>smallint</p></td>
<td><p>使用者在會議工作階段期間所傳送的訊息數。</p></td>
</tr>
</tbody>
</table>

