---
title: TraceRoute 表
TOCTitle: TraceRoute 表
ms:assetid: b9493cef-6ece-4f13-bf68-dbf132aab4f4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205205(v=OCS.15)
ms:contentKeyID: 49292110
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# TraceRoute 表

 

_**上次修改主題的時間：** 2015-03-09_

TraceRoute 表格包含通話的路由資訊。本表已從 Microsoft Lync Server 2013 引進使用。


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
<td><p><strong>ConferenceDateTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>主要，外部</p></td>
<td><p>通話的開始日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要，外部</p></td>
<td><p>用來區別同一日期和同一時間開始之多個通話的唯一識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediaLineLabel</strong></p></td>
<td><p>tinyint</p></td>
<td><p>主要，外部</p></td>
<td><p>代表通話中使用的視訊線路類型。允許的值為：</p>
<ul>
<li><p>0 – 音訊</p></li>
<li><p>1 – 視訊</p></li>
<li><p>2 – 全景視訊</p></li>
<li><p>3 – 應用程式/桌面共用</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>FromCaller</strong></p></td>
<td><p>bit</p></td>
<td><p>主要</p></td>
<td><p>起始通話的端點。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Hop</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>網路躍點/</p></td>
</tr>
<tr class="even">
<td><p><strong>IPAddressKey</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>IP 位址的唯一識別碼。IP 位址資訊儲存在 <a href="lync-server-2013-ipaddress-table.md">Lync Server 2013 中的 IPAddress 表</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RTT</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>來回時間。來回時間測量語音封包抵達目的地接著傳回已接收通知的所需花費時間。</p></td>
</tr>
</tbody>
</table>

