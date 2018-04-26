---
title: Lync Server 2013：Phones 表格
TOCTitle: Phones 表格
ms:assetid: 41cb356d-9cc8-42b6-ac23-98a61b25aadc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425923(v=OCS.15)
ms:contentKeyID: 49290722
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Phones 表格

 

_**上次修改主題的時間：** 2015-03-09_

Phones 表格是一種支援資料表。表格中的每筆記錄儲存一個電話號碼的相關資訊，該電話號碼與在資料庫中有記錄的 VoIP 電話相關。


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
<td><p><strong>PhoneId</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>用於識別此電話的唯一號碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>PhoneUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p> </p></td>
<td><p>電話號碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NextUpdateTS</strong></p></td>
<td><p>日期時間</p></td>
<td><p></p></td>
<td><p>時間戳記 (僅供內部使用)。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
</tbody>
</table>

