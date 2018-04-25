---
title: ClientVersions 檢視
TOCTitle: ClientVersions 檢視
ms:assetid: caf7678f-83a0-46c8-83cc-fee4c3991f52
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721891(v=OCS.15)
ms:contentKeyID: 49890312
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ClientVersions 檢視

 

_**上次修改主題的時間：** 2015-03-09_

ClientVersions 檢視會存放已參與資料庫中所記錄之工作階段的各種用戶端類型與版本的相關資訊。檢視中的每筆記錄代表一個用戶端版本。此檢視已於 Microsoft Lync Server 2013 引進使用。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>特定欄可能有多筆記錄。</td>
</tr>
</tbody>
</table>



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
<td><p><strong>VersionId</strong></p></td>
<td><p>int</p></td>
<td><p>用於識別此用戶端類型及版本的唯一號碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>Version</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>代表使用者代理程式。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientType</strong></p></td>
<td><p>int</p></td>
<td><p>用戶端的類型。</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientCategory</strong></p></td>
<td><p>nvarchar(64)</p></td>
<td><p>用戶端所屬的類別。例如，用戶端 Conferencing_Attendant_1.0 屬於 ClientCategory CAA。</p></td>
</tr>
</tbody>
</table>

