---
title: Lync Server 2013 中的 IPAddress 表
TOCTitle: Lync Server 2013 中的 IPAddress 表
ms:assetid: 8ec018b9-158e-4bbe-ad46-869e60315555
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205077(v=OCS.15)
ms:contentKeyID: 49291631
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 IPAddress 表

 

_**上次修改主題的時間：** 2015-03-09_

IPAddress 表格會將 IP 位址對應至唯一的 IP 位址識別碼，這些識別碼可以在經驗品質資料庫中的任一處使用。本表已從 Microsoft Lync Server 2013 引進使用。


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
<td><p><strong>IPAddressKey</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>指定 IP 位址的唯一識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>IPAddress</strong></p></td>
<td><p>varchar(50)</p></td>
<td><p>唯一</p></td>
<td><p>對應至 IpAddressKey 的唯一 IP 位址 (例如 189.168.1.1)。這可能是 IPv4 或 IPv6 位址。</p></td>
</tr>
</tbody>
</table>

