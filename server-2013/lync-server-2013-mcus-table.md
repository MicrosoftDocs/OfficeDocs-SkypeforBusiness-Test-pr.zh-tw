---
title: Lync Server 2013：Mcus 表格
TOCTitle: Mcus 表格
ms:assetid: 271b7963-8fd8-4d92-a701-1a62aaf895ee
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425742(v=OCS.15)
ms:contentKeyID: 49290405
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Mcus 表格

 

_**上次修改主題的時間：** 2015-03-09_

Mcus 表格是一種支援資料表，其中的每一項記錄都儲存了一個會議服務的資訊。這可能包括 IM 會議服務和電話語音會議服務 (以前端伺服器的程序執行)，以及 Web 會議服務和 A/V 會議服務。


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
<td><p><strong>McuId</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>用於識別此會議伺服器的唯一號碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>McuUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p><strong>McuTypeId</strong></p></td>
<td><p>inyint</p></td>
<td><p>外部</p></td>
<td><p>會議伺服器的類型，例如 conf:chat (針對 IM) 或 conf:audio-video。如需詳細資訊，請參閱＜ <a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>＞。</p></td>
</tr>
</tbody>
</table>

