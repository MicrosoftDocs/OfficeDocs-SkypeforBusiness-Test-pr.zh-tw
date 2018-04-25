---
title: Lync Server 2013 中的 IMReportSummary 表
TOCTitle: Lync Server 2013 中的 IMReportSummary 表
ms:assetid: 27ff9453-53f2-4fae-b637-70a086c9df96
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204753(v=OCS.15)
ms:contentKeyID: 49290392
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 IMReportSummary 表

 

_**上次修改主題的時間：** 2015-03-09_

IMReportSummaryTable 會提供組織中保留之立即訊息工作階段的整體報告。Microsoft Lync Server 2013 中即引入了此資料表。


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
<td><p><strong>StartTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>主要</p></td>
<td><p>立即訊息工作階段開始的日期及時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>TimePeriod</strong></p></td>
<td><p>char(1)</p></td>
<td><p>主要</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p><strong>PoolFQDN</strong></p></td>
<td><p>nvarchar(257)</p></td>
<td><p>主要</p></td>
<td><p>裝載此工作階段之集區的完整網域名稱。</p></td>
</tr>
<tr class="even">
<td><p><strong>AuthType</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>電話的優先順序 (例如，緊急或非緊急)。優先順序資訊會儲存在 <a href="lync-server-2013-callpriorities-table.md">Lync Server 2013 中的 CallPriorities 表格</a> 中。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SessionCount</strong></p></td>
<td><p>bigint</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>MsgCount</strong></p></td>
<td><p>bigint</p></td>
<td><p></p></td>
<td><p>工作階段期間交換的立即訊息總數。</p></td>
</tr>
</tbody>
</table>

