---
title: Lync Server 2013：ProgressReport 表格
TOCTitle: ProgressReport 表格
ms:assetid: 38e5f060-5e9b-4185-87b2-7ef61c4bb75f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425864(v=OCS.15)
ms:contentKeyID: 49290611
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 ProgressReport 表格

 

_**上次修改主題的時間：** 2015-03-09_

進度報告是以通話或工作階段完成時，用戶端上傳至資料庫的資料為基礎。進度報告僅會寫入 Lync Server 2013 判斷為可能對診斷目的有所助益的通話與工作階段。

ErrorTime、ErrorReportSeq 及 ProgressReportSeq 欄位不一定和錯誤有關，而是有關指出通話或訊息狀態的訊息。


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
<td><p><strong>ErrorTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>主要，外部</p></td>
<td><p>包含此進度報告之進度錯誤報告的日期和時間。如需詳細資訊，請參閱＜ <a href="lync-server-2013-errorreport-table.md">Lync Server 2013 中的 ErrorReport 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>ErrorId</strong></p></td>
<td><p>int</p></td>
<td><p>主要，外部</p></td>
<td><p>與 ErrorTime、ProgressReportSeq 搭配使用的識別碼，可識別唯一的進度報告。如需詳細資訊，請參閱＜ <a href="lync-server-2013-errorreport-table.md">Lync Server 2013 中的 ErrorReport 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ErrorReportSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要，外部</p></td>
<td><p>識別錯誤報告的識別碼。ErrorReporSeq 與 ErrorTime 搭配使用，可識別唯一的錯誤報告。如需詳細資訊，請參閱＜ <a href="lync-server-2013-errorreport-table.md">Lync Server 2013 中的 ErrorReport 表格</a>＞。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
<tr class="even">
<td><p><strong>ProgressReportSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>用於識別進度報告的識別碼。與 ErrorTime 及 ErrorReportSeq 搭配使用，可識別唯一的進度報告。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MsDiagId</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>進度報告的診斷 ID。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>傳送錯誤報告的伺服器 (如果是伺服器元件傳送的報告)。如需詳細資訊，請參閱＜ <a href="lync-server-2013-servers-table.md">Lync Server 2013 中的 Servers 表格</a>＞。此欄位推出於 Microsoft Lync Server 2013。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ApplicationId</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>報告針對的 Lync Server 程序。如需詳細資訊，請參閱應用程式表格。</p></td>
</tr>
<tr class="even">
<td><p><strong>詳細資料</strong></p></td>
<td><p>影像</p></td>
<td><p></p></td>
<td><p>進度報告詳細資料，以二進位格式儲存，以節省空間。可使用此語法將資料轉換成文字格式：</p>
<p>cast(cast(Detail as varbinary(max)) as varchar(max))</p></td>
</tr>
<tr class="odd">
<td><p><strong>TelemetryId</strong></p></td>
<td><p>uniqueIdentifier</p></td>
<td><p></p></td>
<td><p>會議所包含之不同元件的加入時間資訊的相互關聯唯一識別碼。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSetupTime</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>特定元件加入會議的時間 (毫秒)。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
</tbody>
</table>

