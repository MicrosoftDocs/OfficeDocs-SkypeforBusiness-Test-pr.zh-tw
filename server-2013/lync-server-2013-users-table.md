---
title: Lync Server 2013：Users 表格
TOCTitle: Users 表格
ms:assetid: a8d71373-4b57-4245-9f02-f7fc0d9fcd3c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412791(v=OCS.15)
ms:contentKeyID: 49291948
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Users 表格

 

_**上次修改主題的時間：** 2015-03-09_

使用者表格是一種支援表格。表格中的每筆記錄都儲存一位使用者的相關資訊，其涉及資料庫中已有記錄的通話或工作階段。


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
<td><p><strong>NextUpdateTS</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>內部使用的時間戳記。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserId</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>用於識別此使用者的唯一號碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p> </p></td>
<td><p>使用者 URI。</p></td>
</tr>
<tr class="even">
<td><p><strong>TenantId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>此使用者的租用戶識別碼。如需詳細資訊，請參閱＜ <a href="lync-server-2013-tenants-table.md">Lync Server 2013 中的 Tenants 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UriTypeId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>此使用者的 URI 類型。如需詳細資訊，請參閱＜ <a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>＞。</p></td>
</tr>
</tbody>
</table>

