---
title: Lync Server 2013：Tenants 表格
TOCTitle: Tenants 表格
ms:assetid: c1b070c1-2c59-4ca9-910b-43f673f97fda
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412950(v=OCS.15)
ms:contentKeyID: 49292214
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Tenants 表格

 

_**上次修改主題的時間：** 2015-03-09_

承租人表格是一種支援表格，儲存了各種承租人的清單。表格中的每筆記錄皆代表一名承租人。

> [!NOTE]  
> 在內部部署中，CDR 會使用內建租用戶識別碼表示各種驗證類型，例如公共 IM 連線、同盟及匿名。




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
<td><p><strong>TenantId</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>識別此租用戶識別碼的唯一號碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>TenantKey</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>允許的值：</p>
<ul>
<li><p>00000000-0000-0000-0000-000000000000 – 企業</p></li>
<li><p>00000000-0000-0000-0000-000000000001 – 同盟</p></li>
<li><p>00000000-0000-0000-0000-000000000002 – 匿名</p></li>
<li><p>00000000-0000-0000-0000-000000000003 – 公用 IM 連線</p></li>
</ul></td>
</tr>
</tbody>
</table>

