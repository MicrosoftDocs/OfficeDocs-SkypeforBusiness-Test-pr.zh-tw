---
title: Lync Server 2013：Server 表格
TOCTitle: Server 表格
ms:assetid: 9af89d08-d35a-48e8-b56d-6df292f973cc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398801(v=OCS.15)
ms:contentKeyID: 49291792
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Server 表格

 

_**上次修改主題的時間：** 2015-03-09_

伺服器表格是一種支援表格。每筆記錄都代表一部伺服器。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>欄</strong></th>
<th><strong>資料類型</strong></th>
<th><strong>索引鍵/索引</strong></th>
<th><strong>詳細資料</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ServerKey</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>識別伺服器的唯一號碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>FQDNOrIP</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>索引</p></td>
<td><p>MAC 位址字串。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ServerType</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>1：中繼伺服器</p>
<p>2：A/V Conferencing Server16394: A/V Edge service32769: Gateway</p></td>
</tr>
<tr class="even">
<td><p><strong>PoolName</strong></p></td>
<td><p>nvarchar(512)</p></td>
<td><p></p></td>
<td><p>伺服器所屬的集區。只適用於 A/V 會議伺服器。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NextUpdateTS</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
</tbody>
</table>

