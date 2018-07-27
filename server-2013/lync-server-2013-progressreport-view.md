---
title: ProgressReport 檢視
TOCTitle: ProgressReport 檢視
ms:assetid: b49f3fc7-0e2f-498f-8505-aaaf54e435f9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721857(v=OCS.15)
ms:contentKeyID: 49890271
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ProgressReport 檢視

 

_**上次修改主題的時間：** 2015-03-09_

ProgressReport 檢視會儲存已完成工作階段的相關資訊。進度報告僅會寫入 Lync Server 2013 判斷為可能對診斷目的有所助益的通話與工作階段。此檢視已於 Microsoft Lync Server 2013 引進使用。

> [!NOTE]  
> ErrorTime、ErrorReportSeq 及 ProgressReportSeq 欄位不一定和錯誤有關，而是有關指出通話或訊息狀態的訊息。




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>資料類型</th>
<th>詳細資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ErrorTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>發生錯誤的時間。當和 ErrorReportSeq 搭配使用時，可以用於找出特定的錯誤。</p></td>
</tr>
<tr class="even">
<td><p><strong>ErrorReportSeq</strong></p></td>
<td><p>int</p></td>
<td><p>用於識別錯誤的識別碼。當和 ErrorTime 搭配使用時，可以用於找出特定的錯誤。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ProgressReportSeq</strong></p></td>
<td><p>int</p></td>
<td><p>用於識別進度報告的識別碼。用於辨別相同錯誤報告的進度報告。</p></td>
</tr>
<tr class="even">
<td><p><strong>MsDiagId</strong></p></td>
<td><p>int</p></td>
<td><p>錯誤報告的診斷識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Source</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>錯誤源自的伺服器名稱 (如果報告是從伺服器元件傳送)。</p></td>
</tr>
<tr class="even">
<td><p><strong>Application</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>錯誤源自的應用程式名稱 (如果報告是從伺服器元件傳送)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>TelemetryId</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>唯一識別碼，其與會議牽涉之不同元件的加入時間資訊相關聯。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSetupTime</strong></p></td>
<td><p>int</p></td>
<td><p>特定元件加入會議所需的時間 (以毫秒為單位)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MsDiagHeader</strong></p></td>
<td><p>varchar(max)</p></td>
<td><p>其他錯誤資訊。</p></td>
</tr>
</tbody>
</table>

