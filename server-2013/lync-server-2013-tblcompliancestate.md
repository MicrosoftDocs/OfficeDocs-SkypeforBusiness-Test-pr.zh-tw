---
title: Lync Server 2013：tblComplianceState
TOCTitle: tblComplianceState
ms:assetid: ea82e56c-3cca-4d89-b4e6-6bcaeb1f2830
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615045(v=OCS.15)
ms:contentKeyID: 49292695
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblComplianceState

 

_**上次修改主題的時間：** 2015-03-09_

tblComplianceState 包含集區全面的相容性狀態資訊。

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
<td><p>lastProcessedEntryID</p></td>
<td><p>bigint，非 NULL</p></td>
<td><p>上次處理規範事件的識別碼。</p></td>
</tr>
<tr class="even">
<td><p>activeServerID</p></td>
<td><p>int，非 null</p></td>
<td><p>保留資料庫上獨佔鎖定之規範伺服器的識別碼，若無則為 -1。</p></td>
</tr>
<tr class="odd">
<td><p>lockExpirationTime</p></td>
<td><p>datetime2，非 NULL</p></td>
<td><p>鎖定到期時間 (如果 activeServerID 不是 -1)。</p></td>
</tr>
</tbody>
</table>

