---
title: Lync Server 2013：Devices 表格
TOCTitle: Devices 表格
ms:assetid: 532e2280-4bbc-4a6c-93da-45d9f80a30a0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398351(v=OCS.15)
ms:contentKeyID: 49290925
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Devices 表格

 

_**上次修改主題的時間：** 2015-03-09_

Devices 表格是一種支援資料表。每筆記錄儲存一部裝置 (電話機) 的資訊。


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
<td><p><strong>DeviceId</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>用於識別此硬體版本的唯一號碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>ManufacturerId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>此裝置的製造商。如需詳細資訊，請參閱＜ <a href="lync-server-2013-manufacturers-table.md">Lync Server 2013 中的 Manufacturers 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HardwareVersionId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>此裝置的硬體版本。如需詳細資訊，請參閱＜ <a href="lync-server-2013-hardwareversions-table.md">Lync Server 2013 中的 HardwareVersions 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>MacAddress</strong></p></td>
<td><p>bigint</p></td>
<td><p></p></td>
<td><p>MAC 位址</p></td>
</tr>
</tbody>
</table>

