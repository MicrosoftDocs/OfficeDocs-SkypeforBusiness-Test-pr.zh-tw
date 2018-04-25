---
title: Lync Server 2013：SessionCorrelation 表格
TOCTitle: SessionCorrelation 表格
ms:assetid: 041705e1-7290-464f-95f8-96256cfa2e3e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398091(v=OCS.15)
ms:contentKeyID: 49289936
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 SessionCorrelation 表格

 

_**上次修改主題的時間：** 2015-03-09_

SessionCorrelation 表格是一種支援資料表。每筆記錄都代表一個用來相互關聯多個工作階段的 CorrelationID。


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
<td><p><strong>總和檢查碼</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>CorrelationKey</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>識別這部 A/V 會議伺服器的唯一號碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CorrelationID</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>唯一</p></td>
<td><p>相互關聯的工作階段會具備相同的 CorrelationID。</p></td>
</tr>
<tr class="even">
<td><p><strong>NextUpdateTS</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>僅限內部使用。</p></td>
</tr>
</tbody>
</table>

