---
title: CodecDescription 表
TOCTitle: CodecDescription 表
ms:assetid: 3598acb8-7ea6-4748-8417-149c971c32a2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204797(v=OCS.15)
ms:contentKeyID: 49290560
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# CodecDescription 表

 

_**上次修改主題的時間：** 2015-03-09_

CodecDescription 表格會將唯一的轉碼器識別碼對應至它們對應的轉碼器。轉碼器可用來為數位訊號編碼以利傳輸與廣播，然後將它們解碼以進行播放。此表格是在 Microsoft Lync Server 2013 中所引進。


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
<td><p><strong>CodecDescriptionKey</strong></p></td>
<td><p>smallint</p></td>
<td><p>主要</p></td>
<td><p>指派給轉碼器的唯一識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>CodecDescription</strong></p></td>
<td><p>varchar(256)</p></td>
<td><p>唯一</p></td>
<td><p>對應至 CodecDescriptionKey 之轉碼器的唯一說明。</p></td>
</tr>
</tbody>
</table>

