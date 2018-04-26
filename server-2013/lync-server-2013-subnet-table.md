---
title: Lync Server 2013：Subnet 表格
TOCTitle: Subnet 表格
ms:assetid: 76f5c995-96c8-4aa3-bc30-1d74991d7c42
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398582(v=OCS.15)
ms:contentKeyID: 49291364
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Subnet 表格

 

_**上次修改主題的時間：** 2015-03-09_

Subnet 表格是一種支援資料表。每筆記錄代表在網路組態設定中定義的一個子網路。


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
<td><p><strong>SubnetIP</strong></p></td>
<td><p>int</p></td>
<td><p>主要，外部</p></td>
<td><p>子網路 IP 的整數表示。</p></td>
</tr>
<tr class="even">
<td><p><strong>SubnetMask</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>子網路遮罩。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserSiteKey</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>參考來源： <a href="lync-server-2013-usersite-table.md">Lync Server 2013 中的 UserSite 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>SubnetDescription</strong></p></td>
<td><p>nvarchar(512)</p></td>
<td><p></p></td>
<td><p>子網路的描述。</p></td>
</tr>
</tbody>
</table>

