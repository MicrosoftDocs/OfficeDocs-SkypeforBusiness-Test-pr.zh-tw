---
title: Lync Server 2013：ContentTypes 表格
TOCTitle: ContentTypes 表格
ms:assetid: e3e38035-457c-4173-bdb9-d53a7420eba2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399007(v=OCS.15)
ms:contentKeyID: 49292601
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 ContentTypes 表格

 

_**上次修改主題的時間：** 2015-03-09_

ContentTypes 是一種支援表格，其中儲存對等工作階段與會議工作階段中都會用到的內容類型清單。表格中的每筆記錄都代表一個內容類型。


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
<td><p><strong>ContentTypeId</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>識別內容類型且不重複的數字。</p></td>
</tr>
<tr class="even">
<td><p><strong>ContentType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td> </td>
<td><p>內容類型名稱。</p></td>
</tr>
</tbody>
</table>

