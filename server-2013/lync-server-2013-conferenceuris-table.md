---
title: Lync Server 2013：ConferenceUris 表格
TOCTitle: ConferenceUris 表格
ms:assetid: b1721d52-3c65-45ea-8997-06af8fef93fc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412854(v=OCS.15)
ms:contentKeyID: 49292040
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 ConferenceUris 表格

 

_**上次修改主題的時間：** 2015-03-09_

ConfereneUris 表格是一種支援表格，其中儲存資料庫中已有參與會議工作階段記錄的各個會議 URI 清單。表格中的每筆記錄都代表一個會議 URI。


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
<td><p><strong>NextUpdateTS</strong></p></td>
<td><p>datetime</p></td>
<td><p>主要</p></td>
<td><p>時間戳記，供內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>ConferenceUriId</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>用於識別此會議 URI 的唯一號碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConferenceUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p></p></td>
<td><p>會議 URI。</p></td>
</tr>
<tr class="even">
<td><p><strong>Checksum</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>ConferenceUri 的總和檢查碼，可用於提升資料庫搜尋速度。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UriTypeId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>URI 類型，如 conf:chat (IM 會議) 或 conf:audio-video (音訊/視訊會議)。如需詳細資訊，請參閱 <a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>。</p></td>
</tr>
</tbody>
</table>

