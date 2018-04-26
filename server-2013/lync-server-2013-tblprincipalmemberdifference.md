---
title: Lync Server 2013：tblPrincipalMemberDifference
TOCTitle: tblPrincipalMemberDifference
ms:assetid: 0b94f555-6888-4fe0-a048-4660a2513276
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558612(v=OCS.15)
ms:contentKeyID: 49290051
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblPrincipalMemberDifference

 

_**上次修改主題的時間：** 2015-03-09_

tblPrincipalMemberDifference 包含稍後 Active Directory 網域服務 同步處理步驟未處理的群組成員資格變更 (已新增及已移除的成員)。

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
<td><p>prinGuid</p></td>
<td><p>GUID，非 null</p></td>
<td><p>已變更群組的主體 GUID。</p></td>
</tr>
<tr class="even">
<td><p>memberADPath</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>成員的辨別名稱。</p></td>
</tr>
<tr class="odd">
<td><p>memberRemoved</p></td>
<td><p>位元，非 null</p></td>
<td><p>False 表示已新增成員；True 表示已移除成員。</p></td>
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
<td><p>&lt;prinGuid, memberADPath&gt;</p></td>
<td><p>主索引鍵。</p></td>
</tr>
</tbody>
</table>

