---
title: Lync Server 2013：UriTypes 表格
TOCTitle: UriTypes 表格
ms:assetid: 77c4dfae-1b29-4e81-ba05-609e61643998
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398587(v=OCS.15)
ms:contentKeyID: 49291375
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 UriTypes 表格

 

_**上次修改主題的時間：** 2015-06-16_

UriTypes 表格包含各種在 Microsoft Lync Server 2013 中受到監控的 URI (統一資源識別項) 類型。


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
<td><p><strong>UriTypeId</strong></p></td>
<td><p>Tinyint</p></td>
<td><p>主要</p></td>
<td><p>指派給 URI 類型的唯一識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>UriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>不同 URI 類型的描述。允許值為：</p>
<ul>
<li><p>0 – Phone Uri</p></li>
<li><p>1 – User Uri</p></li>
</ul></td>
</tr>
</tbody>
</table>

