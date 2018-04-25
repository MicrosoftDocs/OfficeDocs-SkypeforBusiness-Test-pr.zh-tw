---
title: ConferenceUris 檢視
TOCTitle: ConferenceUris 檢視
ms:assetid: 9a3cdcea-426e-4b6b-9876-ba746a8de706
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688148(v=OCS.15)
ms:contentKeyID: 49890224
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ConferenceUris 檢視

 

_**上次修改主題的時間：** 2015-03-09_

ConfernceUris 檢視會儲存已參與會議工作階段之 URI 的相關資訊。此檢視已於 Microsoft Lync Server 2013 引進使用。


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
<td><p>ConferenceUriId</p></td>
<td><p>int</p></td>
<td><p>用於識別會議 URI 的唯一號碼。</p></td>
</tr>
<tr class="even">
<td><p>ConferenceUri</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>會議的 URI。</p></td>
</tr>
<tr class="odd">
<td><p>ConferenceUriType</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>會議 URI 的類型。如需詳細資訊，請參閱 <a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>。</p></td>
</tr>
</tbody>
</table>

