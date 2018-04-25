---
title: Lync Server 2013 中的 UserStatistics 表
TOCTitle: Lync Server 2013 中的 UserStatistics 表
ms:assetid: cfaf803b-1679-4169-92d3-533fad3e56ed
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721893(v=OCS.15)
ms:contentKeyID: 49890323
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 UserStatistics 表

 

_**上次修改主題的時間：** 2015-03-09_

UserStatistics 表格是一種支援表格。表中的每筆記錄會儲存個別使用者的系統使用資訊。本表在 Microsoft Lync Server 2013 中介紹過。


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
<td><p><strong>UserId</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>用於識別此使用者的唯一號碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>LastLogInTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>使用者上次登入的時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LastConfOrganizedTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>使用者上次召集會議的時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>LastCallOrganizerCallFailureTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>使用者上次發生通話失敗的時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LastConfOrganizerCallFailureTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>身為會議召集人的使用者上次發生通話失敗的時。間。</p></td>
</tr>
</tbody>
</table>

