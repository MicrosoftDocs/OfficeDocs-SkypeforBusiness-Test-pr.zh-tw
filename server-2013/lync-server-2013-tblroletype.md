---
title: Lync Server 2013：tblRoleType
TOCTitle: tblRoleType
ms:assetid: 1eac3a54-656a-40ac-b771-edfc64d6e34b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558623(v=OCS.15)
ms:contentKeyID: 49290298
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblRoleType

 

_**上次修改主題的時間：** 2015-03-09_

tblRoleType 表格是一種靜態查閱表格，其中含有角色類型與其相關的權限組。

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
<td><p>rtypeID</p></td>
<td><p>int，非 null</p></td>
<td><p>角色類型識別碼。</p></td>
</tr>
<tr class="even">
<td><p>rtypeDesc</p></td>
<td><p>nvarchar (256)，非 null</p></td>
<td><p>角色類型描述。以下是四個可用的角色：</p>
<ul>
<li><p>Member：聊天室成員</p></li>
<li><p>Manager：聊天室管理員</p></li>
<li><p>Voiced：視聽中心聊天室簡報者</p></li>
<li><p>Creator：可建立聊天室</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>rtypeAllowedPermSet</p></td>
<td><p>bigint，非 NULL</p></td>
<td><p>角色的權限組。使用的位元如下：</p>
<ul>
<li><p>2: 若角色可管理節點則為 True。</p></li>
<li><p>4: 若角色可建立子節點則為 True。</p></li>
<li><p>7: 若角色可加入聊天室 (或類別的子聊天室) 則為 True。</p></li>
<li><p>8: 若角色可在聊天室 (或類別的子聊天室) 中交談則為 True。</p></li>
<li><p>10: 若角色可讀取聊天記錄則為 True (即使未加入聊天室時亦可)。</p></li>
<li><p>11: 若角色可看到聊天室則為 True (可進一步依據範圍和可見度等因素來調整)。</p></li>
<li><p>12: 若角色可在視聽中心聊天室中交談則為 True。</p></li>
<li><p>13: 若角色可在檢視節點時略過可見度規則則為 True。</p></li>
</ul></td>
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
<td><p>rtypeID</p></td>
<td><p>主索引鍵。</p></td>
</tr>
</tbody>
</table>

