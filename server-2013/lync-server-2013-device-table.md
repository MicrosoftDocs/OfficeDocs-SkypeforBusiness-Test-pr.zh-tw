---
title: Lync Server 2013：Device 表格
TOCTitle: Device 表格
ms:assetid: d5a4f777-bc12-4ce8-bc0d-867d5e22b436
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398930(v=OCS.15)
ms:contentKeyID: 49292462
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Device 表格

 

_**上次修改主題的時間：** 2015-03-09_

裝置表格是一種支援表格，儲存了許多擷取與轉換裝置相關資訊。表格中的每筆記錄皆代表一個集區。


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
<td><p><strong>DeviceKey</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>用於識別此裝置的唯一號碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceName</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>DeviceName + DeviceType 是唯一的</p></td>
<td><p>裝置名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceType</strong></p></td>
<td><p>bit</p></td>
<td><p>DeviceName + DeviceType 是唯一的</p></td>
<td><p>裝置類型。1 為擷取裝置，0 為轉譯裝置。</p></td>
</tr>
</tbody>
</table>

