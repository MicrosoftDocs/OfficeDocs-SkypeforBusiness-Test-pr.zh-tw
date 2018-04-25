---
title: Lync Server 2013：tblComplianceFanout
TOCTitle: tblComplianceFanout
ms:assetid: f5d9f342-a7cb-4b54-baa6-e656256b75ad
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615050(v=OCS.15)
ms:contentKeyID: 49292827
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblComplianceFanout

 

_**上次修改主題的時間：** 2015-03-09_

tblComplianceFanout 表格包含已處理規範事件的所有伺服器。

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
<td><p>fanoutEventID</p></td>
<td><p>int</p></td>
<td><p>事件識別碼。</p></td>
</tr>
<tr class="even">
<td><p>fanoutServerID</p></td>
<td><p>int</p></td>
<td><p>伺服器識別 (對應 tblServerIdentity.serverID 表)。</p></td>
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
<td><p>fanoutEventID</p></td>
<td><p>在 tblComplianceData.cmplEventID 表中查閱的外部索引鍵。</p></td>
</tr>
</tbody>
</table>

