---
title: Lync Server 2013：Roles 表格
TOCTitle: Roles 表格
ms:assetid: e8eb8a10-26b5-488b-bc8c-f9ef93f98bdb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399043(v=OCS.15)
ms:contentKeyID: 49292671
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Roles 表格

 

_**上次修改主題的時間：** 2015-03-09_

Roles 表格是儲存可能之會議角色 (例如出席者和簡報者) 清單的靜態表格。


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
<td><p><strong>RoleId</strong></p></td>
<td><p>Tinyint</p></td>
<td><p>主要</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>角色</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>允許的值：</p>
<ul>
<li><p>0 - 未知</p></li>
<li><p>1 - 簡報者</p></li>
<li><p>2 - 出席者</p></li>
</ul></td>
</tr>
</tbody>
</table>

