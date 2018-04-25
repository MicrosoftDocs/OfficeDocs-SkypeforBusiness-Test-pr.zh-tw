---
title: Lync Server 2013：ConferenceMessageCount 表格
TOCTitle: ConferenceMessageCount 表格
ms:assetid: 78569dbf-5217-42fa-ba1a-4380f56e2a3d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398590(v=OCS.15)
ms:contentKeyID: 49291382
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 ConferenceMessageCount 表格

 

_**上次修改主題的時間：** 2015-03-09_

此表格中的每筆記錄代表一個 IM 會議中的一位使用者，並包含該使用者傳送的訊息數目。每個會議會由此表格中的多筆記錄來表示，其中每筆記錄代表一位使用者。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>資料類型</th>
<th>索引鍵/索引</th>
<th>詳細資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>主要，外部</p></td>
<td><p>會議執行個體的時間。會與 <strong>SessionIdSeq</strong> 搭配使用，專門用於識別會議執行個體。如需詳細資訊，請參閱＜ <a href="lync-server-2013-conferences-table.md">Lync Server 2013 中的 Conferences 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要，外部</p></td>
<td><p>用於識別會議執行個體的識別碼。會與 <strong>SessionIdTime</strong> 搭配使用，專門用於識別會議執行個體。如需詳細資訊，請參閱＜ <a href="lync-server-2013-conferences-table.md">Lync Server 2013 中的 Conferences 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>用於識別此使用者的唯一號碼。參考來源： <a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>MessageCount</strong></p></td>
<td><p>smallint</p></td>
<td><p> </p></td>
<td><p>本會議中這位使用者所傳送的訊息數。</p></td>
</tr>
</tbody>
</table>

