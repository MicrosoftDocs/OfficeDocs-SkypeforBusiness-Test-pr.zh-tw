---
title: User 檢視
TOCTitle: User 檢視
ms:assetid: 796f77e6-1da6-4969-b18b-3537209a1fe4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688100(v=OCS.15)
ms:contentKeyID: 49890124
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# User 檢視

 

_**上次修改主題的時間：** 2015-03-09_

使用者檢視會儲存在資料庫中有記錄之通話或工作階段中所涉及的使用者相關資訊。此檢視是在 Microsoft Lync Server 2013 中所引進。


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
<td><p>UserId</p></td>
<td><p>int</p></td>
<td><p>用於識別此使用者的唯一號碼。</p></td>
</tr>
<tr class="even">
<td><p>UserUri</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>使用者的 URI。</p></td>
</tr>
<tr class="odd">
<td><p>TenantKey</p></td>
<td><p>uniqueidentifier</p></td>
<td><p>使用者的租用戶。請參閱 <a href="lync-server-2013-tenants-table.md">Lync Server 2013 中的 Tenants 表格</a>，以取得更多資訊。</p></td>
</tr>
<tr class="even">
<td><p>UriType</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>使用者 URI 的類型。請參閱 <a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>，以取得更多資訊。</p></td>
</tr>
</tbody>
</table>

