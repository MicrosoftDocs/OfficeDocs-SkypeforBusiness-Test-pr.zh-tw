---
title: Lync Server 2013：AppliedBandwidthSource 表格
TOCTitle: AppliedBandwidthSource 表格
ms:assetid: 24fb3caf-19b3-4c0a-90d7-ca5d53de32ad
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425725(v=OCS.15)
ms:contentKeyID: 49290364
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 AppliedBandwidthSource 表格

 

_**上次修改主題的時間：** 2015-03-09_

AppliedBandwidthSource 表格是一種支援資料表，其中的每一項記錄都代表一種來源。


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
<td><p><strong>AppliedBandwidthSourceKey</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>用於識別來源的唯一號碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>AppliedBandwidthSource</strong></p></td>
<td><p>varchar(256)</p></td>
<td><p>唯一</p></td>
<td><p>這是所採用的頻寬容量來源。其會說明頻寬限制的來源 (例如，「原則伺服器」、「TURN 伺服器」或「形式」)。</p></td>
</tr>
</tbody>
</table>

