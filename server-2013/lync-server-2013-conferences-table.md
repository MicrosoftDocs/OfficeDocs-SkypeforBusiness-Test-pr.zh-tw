---
title: Lync Server 2013：Conferences 表格
TOCTitle: Conferences 表格
ms:assetid: c3da6271-b3c6-4898-894f-10456ec794d0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412964(v=OCS.15)
ms:contentKeyID: 49292230
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Conferences 表格

 

_**上次修改主題的時間：** 2015-03-09_

此表格中的每筆記錄均包含一場電話會議的通話詳細資訊。


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
<td><p>主要</p></td>
<td><p>CDR 代理程式擷取會議要求的時間。其只會用為主索引鍵，是會議執行個體的專用識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>識別工作階段的識別碼，會與 <strong>SessionIdTime</strong> 並用，是會議執行個體的專用識別碼。*</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConferenceUriId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>會議 URI。如需詳細資訊，請參閱 <a href="lync-server-2013-conferenceuris-table.md">Lync Server 2013 中的 ConferenceUris 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>ConfInstance</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p> </p></td>
<td><p>可用於週期性會議；每一個週期性會議執行個體的 <strong>ConferenceUri</strong> 皆相同，但 <strong>ConfInstance</strong> 則各不相同。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConferenceStartTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>會議結束時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>ConferenceEndTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>會議結束時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PoolId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>識別擷取的會議所在之集區的識別碼。如需詳細資訊，請參閱 <a href="lync-server-2013-pools-table.md">Lync Server 2013 中的 Pools 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>OrganizerId</strong></p></td>
<td><p>Int</p></td>
<td><p>外部</p></td>
<td><p>識別此會議之召集人 URI 的識別碼。如需詳細資訊，請參閱 <a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>旗標</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>包含會議屬性的位元遮罩。可能的值有：</p>
<ul>
<li><p>0X01</p></li>
<li><p>綜合</p></li>
<li><p>交易</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>已處理</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>監控服務所使用的內部欄位。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
</tbody>
</table>


\* 大部分工作階段的 SessionIdSeq 值皆會是 1。如有兩個工作階段的開始時間完全相同，其中一個工作階段的 SessionIdSeq 值會是 1，另一個則會是 2，依此類推。

