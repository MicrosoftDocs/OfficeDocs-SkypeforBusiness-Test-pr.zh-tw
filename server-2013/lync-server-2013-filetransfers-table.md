---
title: Lync Server 2013：FileTransfers 表格
TOCTitle: FileTransfers 表格
ms:assetid: 5368e67c-d8a9-43a1-9472-a839950dedb3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398353(v=OCS.15)
ms:contentKeyID: 49290928
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 FileTransfers 表格

 

_**上次修改主題的時間：** 2015-03-09_

每筆記錄代表一個檔案傳輸工作階段。


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
<td><p>工作階段要求的時間，會與 <strong>SessionIdSeq</strong> 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱＜ <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要，外部</p></td>
<td><p>識別工作階段的識別碼，其會與 <strong>SessionIdTime</strong> 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱 <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>檔案名稱</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>檔案的名稱。</p></td>
</tr>
<tr class="even">
<td><p><strong>FileIdentity</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p></p></td>
<td><p>傳輸同一檔名的檔案時，方便識別的唯一識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Cookie</strong></p></td>
<td><p>nvarchar(128)</p></td>
<td><p>主要</p></td>
<td><p>可用來識別與此訊息相關聯的每則後續訊息。</p></td>
</tr>
<tr class="even">
<td><p><strong>接受</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>可為 TRUE 或 NULL。若為 TRUE，則「拒絕」和「取消」為 NULL。</p></td>
</tr>
<tr class="odd">
<td><p><strong>拒絕</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>可為 TRUE 或 NULL。若為 TRUE，則「接受」和「取消」為 NULL。</p></td>
</tr>
<tr class="even">
<td><p><strong>取消</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>可為 TRUE 或 NULL。若為 TRUE，則「接受」和「拒絕」為 NULL。</p></td>
</tr>
</tbody>
</table>

