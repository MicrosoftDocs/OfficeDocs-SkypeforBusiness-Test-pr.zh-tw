---
title: Conferences 檢視
TOCTitle: Conferences 檢視
ms:assetid: c0e5c4db-c135-401f-9296-e9a49f6499a1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721871(v=OCS.15)
ms:contentKeyID: 49890289
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Conferences 檢視

 

_**上次修改主題的時間：** 2015-03-09_

「會議檢視」會存放會議的相關資訊。此檢視已於 Microsoft Lync Server 2013 引進使用。


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
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>日期時間</p></td>
<td><p>工作階段要求的時間。 當和 SessionIdSeq 搭配使用時，可用於找出特定的工作階段。如需詳細資訊，請參閱 <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>識別工作階段的識別碼。當和 SessionIdTime 搭配使用時，可用於找出特定的工作階段。如需詳細資訊，請參閱<a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConferenceUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>會議的 URI。</p></td>
</tr>
<tr class="even">
<td><p><strong>ConferenceUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>會議 URI 的類型。如需詳細資訊，請參閱 <a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConfInstance</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>用於週期性會議。週期性會議的每個執行個體均具有相同的 ConferenceUri，但是具有不同的 ConfInstance。</p></td>
</tr>
<tr class="even">
<td><p><strong>ConferenceStartTime</strong></p></td>
<td><p>日期時間</p></td>
<td><p>會議的開始時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConferenceEndTime</strong></p></td>
<td><p>日期時間</p></td>
<td><p>會議的結束時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>OrganizerUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>召開會議之使用者的 URI。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OrganizerType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>召開會議之使用者的 URI 類型。如需詳細資訊，請參閱 <a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>OrganizerTenant</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>召開會議之使用者的租用戶。 如需詳細資訊，請參閱 <a href="lync-server-2013-tenants-table.md">Lync Server 2013 中的 Tenants 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Pool</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>裝載會議之集區的完整網域名稱。</p></td>
</tr>
<tr class="even">
<td><p><strong>Flag</strong></p></td>
<td><p>smallint</p></td>
<td><p>包含會議屬性的位元遮罩。可能的值有：</p>
<p>0X01 – 綜合交易</p></td>
</tr>
</tbody>
</table>

