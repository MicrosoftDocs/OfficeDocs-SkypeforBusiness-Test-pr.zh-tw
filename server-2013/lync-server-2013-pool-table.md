---
title: Lync Server 2013：Pool 表格
TOCTitle: Pool 表格
ms:assetid: 92ded8fd-d0ad-4f8a-9e6f-2e8a690fda3a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398746(v=OCS.15)
ms:contentKeyID: 49291682
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Pool 表格

 

_**上次修改主題的時間：** 2015-03-09_

集區表格是一種支援表格，其中儲存不同的前端集區相關資訊。表格中的每筆記錄都代表一個集區。


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
<td><p><strong>PoolKey</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>用於識別此集區的唯一號碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>PoolName</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>唯一</p></td>
<td><p>集區的 FQDN。</p></td>
</tr>
</tbody>
</table>

