---
title: Lync Server 2013：Conference 表格
TOCTitle: Conference 表格
ms:assetid: 2a2c327c-4719-42dc-a3bb-6dbc0864d9af
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425762(v=OCS.15)
ms:contentKeyID: 49290425
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Conference 表格

 

_**上次修改主題的時間：** 2015-03-09_

會議表格是一種支援資料表，其中的每一項記錄都代表一個會議或對等工作階段。


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
<td><p><strong>ConferenceKey</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>用於識別此會議記錄的唯一號碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>ConfURI</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>唯一</p></td>
<td><p>如果是會議則為會議 URI，如果是對等工作階段則為 DialogID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Checksum</strong></p></td>
<td><p>int</p></td>
<td><p>索引</p></td>
<td><p>會議 URI 的總和檢查碼。僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>NextUpdateTS</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
</tbody>
</table>

