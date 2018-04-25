---
title: Lync Server 2013：CallType 表格
TOCTitle: CallType 表格
ms:assetid: a1d7187c-f851-4967-88ea-73922911ee7a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412752(v=OCS.15)
ms:contentKeyID: 49291848
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 CallType 表格

 

_**上次修改主題的時間：** 2015-03-09_

CallType 表格是儲存可能之通話類型清單的靜態表格。


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
<td><p><strong>CallTypeId</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>CallType</strong></p></td>
<td><p>nvarchar</p></td>
<td><p></p></td>
<td><p>允許的值：</p>
<ul>
<li><p>0 – 未知</p></li>
<li><p>1 – 立即訊息</p></li>
<li><p>2 – 應用程式共用</p></li>
<li><p>3 – 音訊</p></li>
<li><p>4 – 音訊與視訊</p></li>
<li><p>5 – 檔案傳輸</p></li>
</ul></td>
</tr>
</tbody>
</table>

