---
title: Media 檢視
TOCTitle: Media 檢視
ms:assetid: 1a7b2e59-082e-4188-98ae-48ae9bd3494a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687981(v=OCS.15)
ms:contentKeyID: 49889961
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Media 檢視

 

_**上次修改主題的時間：** 2015-03-09_

媒體檢視可儲存對等工作階段中所使用之一種媒體類型的相關資訊。若某階段工作使用了一種以上的媒體類型，則在表格中會呈現多個記錄。Microsoft Lync Server 2013 中即引入了此檢視。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您不應使用媒體檢視來計算工作階段的媒體持續期間。此檢視包含工作階段中的媒體交換訊號詳細資料。媒體交換是由 INVITE 要求來執行，且 StartTime 會指出 INVITE 傳送出來的時間。邀請時間不一定表示媒體開始時間，因為只有在接受工作階段後，媒體才會開始。</td>
</tr>
</tbody>
</table>


除了以下所示的欄位以外，媒體檢視還包含＜[SessionDetails 檢視](lync-server-2013-sessiondetails-view.md)＞中的所有欄。


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
<td><p><strong>媒體</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>媒體類型。如需詳細資訊，請參閱＜<a href="lync-server-2013-medialist-table.md">Lync Server 2013 中的 MediaList 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>MediaStartTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>媒體要求傳送出來的時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediaEndTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>工作階段結束時間。</p></td>
</tr>
</tbody>
</table>

