---
title: Lync Server 2013：MediaList 表格
TOCTitle: MediaList 表格
ms:assetid: 1f440590-c1bc-483e-b7bc-6cc763847768
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398279(v=OCS.15)
ms:contentKeyID: 49290296
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 MediaList 表格

 

_**上次修改主題的時間：** 2015-03-09_

MediaList 表格是一種靜態表格，其中儲存了各種媒體類型清單。


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
<td><p><strong>MediaId</strong></p></td>
<td><p>tinyint</p></td>
<td><p>主要</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>Media</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>允許的值：</p>
<ul>
<li><p>1 – IM</p></li>
<li><p>2 – 檔案傳輸</p></li>
<li><p>3 – 遠端協助</p></li>
<li><p>4 – 應用程式共用</p></li>
<li><p>5 – 音訊</p></li>
<li><p>6 – 視訊</p></li>
<li><p>7 – 應用程式邀請</p></li>
</ul></td>
</tr>
</tbody>
</table>

