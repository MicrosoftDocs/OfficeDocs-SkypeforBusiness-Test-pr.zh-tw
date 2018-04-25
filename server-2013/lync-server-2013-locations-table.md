---
title: Lync Server 2013：Locations 表格
TOCTitle: Locations 表格
ms:assetid: 78dc1b14-5394-4f8e-89d3-4ba593272a04
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398596(v=OCS.15)
ms:contentKeyID: 49291394
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Locations 表格

 

_**上次修改主題的時間：** 2015-03-09_

每筆記錄代表緊急通話中參照的一個位置，例如 E9-1-1 通話。


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
<td><p><strong>位置</strong></p></td>
<td><p>nvarchar (max)</p></td>
<td><p></p></td>
<td><p>緊急電話的位置。</p></td>
</tr>
</tbody>
</table>

