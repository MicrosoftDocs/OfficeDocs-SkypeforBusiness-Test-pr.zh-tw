---
title: Lync Server 2013：媒體資料表格
TOCTitle: 媒體資料表格
ms:assetid: 1e1b427f-59b5-4564-bde5-1002a80439ee
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398268(v=OCS.15)
ms:contentKeyID: 49290279
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的媒體資料表格

 

_**上次修改主題的時間：** 2015-03-09_

每一項記錄都代表對等工作階段所用的一種媒體類型。若某階段工作使用了一種以上的媒體類型，則在表格中會呈現多個記錄。

> [!NOTE]  
> 您不應使用媒體資料表來計算工作階段的媒體持續期間。此資料表包含工作階段中的媒體交換訊號詳細資料。媒體交換是由 INVITE 要求來執行，且 StartTime 會指出 INVITE 傳送出來的時間。邀請時間不一定表示媒體開始時間，因為只有在接受工作階段後，媒體才會開始。EndTime 通常是指此工作階段的結束時間。




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
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>主要，外部</p></td>
<td><p>工作階段要求的時間，會與 <strong>SessionIdSeq</strong> 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱＜ <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要，外部</p></td>
<td><p>識別工作階段的識別碼，其會與 <strong>SessionIdTime</strong> 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱 <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediaId</strong></p></td>
<td><p>Tinyint</p></td>
<td><p>主要，外部</p></td>
<td><p>用於識別此媒體類型的唯一號碼。如需詳細資訊，請參閱＜ <a href="lync-server-2013-medialist-table.md">Lync Server 2013 中的 MediaList 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>StartTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>主要</p></td>
<td><p>這是媒體要求傳送出來的時間，而不是實際的媒體開始時間。 <strong>StartTime</strong> 會指出工作階段開始時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EndTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>這是工作階段結束時間。</p></td>
</tr>
</tbody>
</table>

