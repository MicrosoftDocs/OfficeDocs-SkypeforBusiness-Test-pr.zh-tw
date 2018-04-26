---
title: Lync Server 2013：tblConfig
TOCTitle: tblConfig
ms:assetid: 7445e7db-c574-46fa-b964-8640d77047a8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558663(v=OCS.15)
ms:contentKeyID: 49291334
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblConfig

 

_**上次修改主題的時間：** 2015-03-09_

在某一列中，tblConfig 包含部分 常設聊天室伺服器 未支援的設定。

### 欄

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>configLabel</p></td>
<td><p>nvarchar (255)，非 null</p></td>
<td><p>包含「集區」。</p></td>
</tr>
<tr class="even">
<td><p>configContent</p></td>
<td><p>nvarchar (max)</p></td>
<td><p>設定內容。</p></td>
</tr>
<tr class="odd">
<td><p>configPoolID</p></td>
<td><p>GUID，非 null</p></td>
<td><p>資料庫執行個體的唯一識別碼。</p></td>
</tr>
</tbody>
</table>


### 索引鍵

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>configLabel</p></td>
<td><p>主索引鍵。</p></td>
</tr>
</tbody>
</table>

