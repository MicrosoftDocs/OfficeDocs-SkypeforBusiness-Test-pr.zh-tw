---
title: Lync Server 2013 中的 ErrorCategory 表
TOCTitle: Lync Server 2013 中的 ErrorCategory 表
ms:assetid: 0fde3b73-9a2f-44dd-b8dc-6df512303ff1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204675(v=OCS.15)
ms:contentKeyID: 49290112
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 ErrorCategory 表

 

_**上次修改主題的時間：** 2015-03-09_

ErrorCategory 表格包含每個 Microsoft Lync Server 2013 診斷分類的易記名稱。依預設，Lync Server 2013 會使用下列分類：

  - 0 -- 成功

  - 1 -- 預期的失敗

  - 2 – 未預期的失敗

Microsoft Lync Server 2013 中即引入了此資料表。


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
<td><p><strong>CategoryID</strong></p></td>
<td><p>tinyint</p></td>
<td><p>主要</p></td>
<td><p>分類的唯一識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>名稱</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>指派給分類的值和易記名稱。允許的值為：</p>
<ul>
<li><p>0 -- 成功</p></li>
<li><p>1 -- 預期的失敗</p></li>
<li><p>2 – 未預期的失敗</p></li>
</ul></td>
</tr>
</tbody>
</table>

