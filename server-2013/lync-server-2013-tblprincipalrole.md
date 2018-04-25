---
title: Lync Server 2013：tblPrincipalRole
TOCTitle: tblPrincipalRole
ms:assetid: dcd16dc1-a66c-4720-a48f-ec8b28337383
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615039(v=OCS.15)
ms:contentKeyID: 49292534
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblPrincipalRole

 

_**上次修改主題的時間：** 2015-03-09_

tblPrincipalRole 包含指派給節點的明確角色。

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
<td><p>prinRoleNodeID</p></td>
<td><p>int，非 null</p></td>
<td><p>套用角色之節點識別碼。</p></td>
</tr>
<tr class="even">
<td><p>prinRolePrinID</p></td>
<td><p>int，非 null</p></td>
<td><p>主體識別碼。</p></td>
</tr>
<tr class="odd">
<td><p>prinRoleTypeID</p></td>
<td><p>int，非 null</p></td>
<td><p>角色類型識別碼 (來自於 tblRoleType)。</p></td>
</tr>
<tr class="even">
<td><p>prinRoleUpdatedBy</p></td>
<td><p>int，非 null</p></td>
<td><p>上次更新此項目之主體的識別碼。</p></td>
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
<td><p>&lt;prinRoleNodeID, prinRolePrinID, prinRoleTypeID&gt;</p></td>
<td><p>主索引鍵。</p></td>
</tr>
<tr class="even">
<td><p>prinRoleNodeID</p></td>
<td><p>在 tblNode.nodeID 表格中查閱外部索引鍵。</p></td>
</tr>
<tr class="odd">
<td><p>prinRolePrinID</p></td>
<td><p>在 tblPrincipal.prinID 表格中查閱外部索引鍵。</p></td>
</tr>
<tr class="even">
<td><p>prinRoleTypeID</p></td>
<td><p>在 tblRoleType.rtypeID 表格中查閱外部索引鍵。</p></td>
</tr>
</tbody>
</table>

