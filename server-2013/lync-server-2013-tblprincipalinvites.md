---
title: Lync Server 2013：tblPrincipalInvites
TOCTitle: tblPrincipalInvites
ms:assetid: 548ec156-4d1a-469d-a804-62cff226e5c2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558650(v=OCS.15)
ms:contentKeyID: 49290943
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblPrincipalInvites

 

_**上次修改主題的時間：** 2015-03-09_

tblPrincipalInvites 包含所有提供給啟動自動邀請的所有節點之佈建使用者的邀請。

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
<td><p>prinID</p></td>
<td><p>int，非 null</p></td>
<td><p>主體識別碼。</p></td>
</tr>
<tr class="even">
<td><p>invID</p></td>
<td><p>int，非 null</p></td>
<td><p>從 tblLastInviteId 表格產生的唯一序號 (每個主體識別碼)。</p></td>
</tr>
<tr class="odd">
<td><p>nodeID</p></td>
<td><p>int，非 null</p></td>
<td><p>節點識別碼 (僅限聊天室)。</p></td>
</tr>
<tr class="even">
<td><p>createdOn</p></td>
<td><p>日期時間，非 null</p></td>
<td><p>建立的時間。</p></td>
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
<td><p>&lt;prinID, nodeID&gt;</p></td>
<td><p>主索引鍵。</p></td>
</tr>
<tr class="even">
<td><p>prinID</p></td>
<td><p>在 tblPrincipal.prinID 表格中查閱外部索引鍵。</p></td>
</tr>
<tr class="odd">
<td><p>nodeID</p></td>
<td><p>在 tblNode.nodeID 表格中查閱外部索引鍵。</p></td>
</tr>
</tbody>
</table>

