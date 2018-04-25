---
title: Lync Server 2013：PayloadDescription 表格
TOCTitle: PayloadDescription 表格
ms:assetid: c49d61c0-305a-4770-a5d2-5d9f05decc6d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412971(v=OCS.15)
ms:contentKeyID: 49292251
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 PayloadDescription 表格

 

_**上次修改主題的時間：** 2015-03-09_

PayloadDescription 表格是一種支援表格。每筆記錄都代表一個用於音訊或視訊工作階段的轉碼器。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>欄</strong></th>
<th><strong>資料類型</strong></th>
<th><strong>索引鍵/索引</strong></th>
<th><strong>詳細資料</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>PayloadDescriptionKey</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>轉碼器的識別專用號碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>PayloadDescription</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>唯一</p></td>
<td><p>轉碼器名稱。</p></td>
</tr>
</tbody>
</table>

