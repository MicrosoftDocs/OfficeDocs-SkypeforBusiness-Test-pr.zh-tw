---
title: Lync Server 2013：Dialog 表格
TOCTitle: Dialog 表格
ms:assetid: 4d93424f-9072-43f5-83c2-3d539e3e9ca6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398313(v=OCS.15)
ms:contentKeyID: 49290869
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Dialog 表格

 

_**上次修改主題的時間：** 2015-03-09_

Dialog 表格是一種支援資料表；每筆記錄代表一個工作階段初始通訊協定 (SIP) 對話方塊。


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
<td><p><strong>ConferenceDateTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>主要</p></td>
<td><p>卓越品質 (Quality of Excellence, QoE) 代理程式從發話者或受話者收到第一份報告的時間。其會與 SessionSeq 搭配使用，專門用於識別工作階段。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>當工作階段的 ConferenceDateTime 相同時，用來區分工作階段的序號。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DialogID</strong></p></td>
<td><p>varchar(256)</p></td>
<td><p></p></td>
<td><p>全域唯一的對話方塊 ID。</p></td>
</tr>
<tr class="even">
<td><p><strong>DialogIDChecksum</strong></p></td>
<td><p>int</p></td>
<td><p>索引</p></td>
<td><p>對話方塊 ID 的總和檢查碼。</p></td>
</tr>
</tbody>
</table>

