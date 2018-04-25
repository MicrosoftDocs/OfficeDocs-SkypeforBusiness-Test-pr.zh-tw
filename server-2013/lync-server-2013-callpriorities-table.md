---
title: Lync Server 2013：CallPriorities 表格
TOCTitle: CallPriorities 表格
ms:assetid: 043b63ae-2d64-4f38-a0df-18aa08d6caf5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398093(v=OCS.15)
ms:contentKeyID: 49289939
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 CallPriorities 表格

 

_**上次修改主題的時間：** 2015-03-09_

CallPriorities 表格是靜態表格，可儲存通話可能優先順序的清單 (如「緊急」、「急」或「一般」)。


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
<td><p><strong>PriorityId</strong></p></td>
<td><p>Tinyint</p></td>
<td><p>主要</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>優先順序</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>允許的值：</p>
<ul>
<li><p>0 - 未知</p></li>
<li><p>1 - 非緊急</p></li>
<li><p>2 - 一般</p></li>
<li><p>3 - 急</p></li>
<li><p>4 - 緊急</p></li>
</ul></td>
</tr>
</tbody>
</table>

