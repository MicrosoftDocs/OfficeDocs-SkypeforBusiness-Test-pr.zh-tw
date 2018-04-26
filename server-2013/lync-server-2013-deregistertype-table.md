---
title: Lync Server 2013：DeRegisterType 表格
TOCTitle: DeRegisterType 表格
ms:assetid: 09148118-6209-4fd7-a494-99118689a245
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398142(v=OCS.15)
ms:contentKeyID: 49290021
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 DeRegisterType 表格

 

_**上次修改主題的時間：** 2015-03-09_

DeRegisterType 表格是靜態表格，可儲存使用者取消註冊可能類型的清單 (如「由用戶端起始」、「註冊到期」或「用戶端停止回應」)。


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
<td><p><strong>DeRegisterTypeId</strong></p></td>
<td><p>Tinyint</p></td>
<td><p>主要</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>DeRegisterReason</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>允許的值：</p>
<ul>
<li><p>0 – 未知</p></li>
<li><p>1 – 由用戶端起始取消註冊</p></li>
<li><p>2 – 註冊到期</p></li>
<li><p>3 – 用戶端損毀</p></li>
<li><p>4 – 使用者屬性變更</p></li>
<li><p>5 – 慣用的登錄器變更</p></li>
<li><p>6 – 舊版用戶端處於生存模式</p></li>
</ul></td>
</tr>
</tbody>
</table>

