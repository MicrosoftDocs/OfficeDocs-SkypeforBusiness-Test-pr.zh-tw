---
title: Lync Server 2013 中的 NetworkConnectionDetail 表
TOCTitle: Lync Server 2013 中的 NetworkConnectionDetail 表
ms:assetid: b48cc9a6-5232-48b5-bd20-53b68229336b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205185(v=OCS.15)
ms:contentKeyID: 49292064
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 NetworkConnectionDetail 表

 

_**上次修改主題的時間：** 2015-03-09_

NetworkConnectionDetail 表格會將網路連線類型對應到「經驗品質」資料庫中其他地方使用的網路連線識別碼。本表已從 Microsoft Lync Server 2013 引進使用。


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
<td><p><strong>NetworkConnectionDetailKey</strong></p></td>
<td><p>tinyint</p></td>
<td><p>主要</p></td>
<td><p>網路連線類型的唯一識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>NetworkConnectionDetail</strong></p></td>
<td><p>varchar(256)</p></td>
<td><p>唯一</p></td>
<td><p>對應到 NetworkConnectionDetailKey 的網路連線類型。允許的值為：</p>
<ol>
<li><p>0 -- 有線</p></li>
<li><p>1 -- WiFi</p></li>
<li><p>2 -- 乙太網路</p></li>
</ol></td>
</tr>
</tbody>
</table>

