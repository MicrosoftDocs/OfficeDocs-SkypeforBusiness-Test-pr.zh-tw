---
title: Lync Server 2013：tblPrincipalAffiliations
TOCTitle: tblPrincipalAffiliations
ms:assetid: 45fd8484-5837-44d2-85bb-45c83546607c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558642(v=OCS.15)
ms:contentKeyID: 49290779
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblPrincipalAffiliations

 

_**上次修改主題的時間：** 2015-03-09_

PrincipalAffiliations 包含主體關係，可描述位置 (包括 Active Directory 網域服務 安全性群組)、Active Directory 容器及網域中的成員資格。

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
<td><p>principalID</p></td>
<td><p>int，非 null</p></td>
<td><p>相關主體的識別碼。</p></td>
</tr>
<tr class="even">
<td><p>affiliationID</p></td>
<td><p>int，非 null</p></td>
<td><p>代表關係的主體識別碼。每個主體 (系統使用者類型除外) 也都具有自我關係。</p></td>
</tr>
<tr class="odd">
<td><p>索引</p></td>
<td><p>int，非 null</p></td>
<td><p>索引。自我關係的值為 -1，其他關係的值則是在每個 &lt;principalID, affiliationId&gt; 值區內，從 1 開始依序增加。</p></td>
</tr>
<tr class="even">
<td><p>updatedBy</p></td>
<td><p>int，非 null</p></td>
<td><p>已執行最新更新的主體。這通常是 1，表示 Active Directory 同步處理。</p></td>
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
<td><p>&lt;principalID, index, affiliationID&gt;</p></td>
<td><p>主索引鍵。</p></td>
</tr>
<tr class="even">
<td><p>principalID</p></td>
<td><p>在 tblPrincipal.prinID 表格中查閱外部索引鍵。</p></td>
</tr>
<tr class="odd">
<td><p>affiliationID</p></td>
<td><p>在 tblPrincipal.prinID 表格中查閱外部索引鍵。</p></td>
</tr>
</tbody>
</table>

