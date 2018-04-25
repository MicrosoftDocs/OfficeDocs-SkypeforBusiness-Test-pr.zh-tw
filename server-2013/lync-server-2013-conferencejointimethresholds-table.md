---
title: Lync Server 2013 中的 ConferenceJoinTimeThresholds 表
TOCTitle: Lync Server 2013 中的 ConferenceJoinTimeThresholds 表
ms:assetid: 3944d724-bdd8-4d1c-a2af-933ee8141529
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204809(v=OCS.15)
ms:contentKeyID: 49290623
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 ConferenceJoinTimeThresholds 表

 

_**上次修改主題的時間：** 2015-03-09_

ConferenceJoinTimeThresholds 表格中包含「會議加入時間摘要報告」所使用的分類界限。「會議加入時間摘要報告」摘要說明了使用者成功加入會議所需的時間；在報告中這些時間值會以平均值及下列其中一項類別表示：

  - 少於 2 秒。

  - 介於 2 秒和 5 秒之間。

  - 介於 5 秒和 10 秒之間。

  - 超過 10 秒。

ConferenceJoinTimeThresholds 表格包含 2 秒、5 秒及 10 秒的分類值。

此表格推出於 Microsoft Lync Server 2013。


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
<td><p><strong>ThresholdId</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>分類的唯一識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>ThresholdValue</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>分類的上限。允許的值為：</p>
<ol>
<li><p>2</p></li>
<li><p>5</p></li>
<li><p>10</p></li>
</ol></td>
</tr>
</tbody>
</table>

