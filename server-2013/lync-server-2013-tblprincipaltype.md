---
title: Lync Server 2013：tblPrincipalType
TOCTitle: tblPrincipalType
ms:assetid: 32e1c1d6-80f4-4624-bf4e-b4c77d3982fa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558633(v=OCS.15)
ms:contentKeyID: 49290524
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblPrincipalType

 

_**上次修改主題的時間：** 2015-03-09_

tblPrincipalType 含有主要類型以分類 tblPrincipal 表格中的項目。

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
<td><p>ptypeID</p></td>
<td><p>smallint，非 null</p></td>
<td><p>主體類型識別碼。</p></td>
</tr>
<tr class="even">
<td><p>ptypeDesc</p></td>
<td><p>nvarchar (256)，非 null</p></td>
<td><p>類型的描述。</p></td>
</tr>
<tr class="odd">
<td><p>ptypeIsSystemUser</p></td>
<td><p>位元，非 null</p></td>
<td><p>如果類型對應至作為內部用途的主體，則為 True。</p></td>
</tr>
<tr class="even">
<td><p>ptypeIsUser</p></td>
<td><p>位元，非 null</p></td>
<td><p>如果類型為使用者類型，則為 True。</p></td>
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
<td><p>ptypeID</p></td>
<td><p>主索引鍵。</p></td>
</tr>
</tbody>
</table>


### 主體值

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ID</th>
<th>角色</th>
<th>說明</th>
<th>使用者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>任何一個</p></td>
<td><p>不含已知類型的一般主體。不使用在 tblPrincipal 表格中。</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>AnyUser</p></td>
<td><p>使用者類型的一般主體。不使用在 tblPrincipal 表格中。</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p>AnyGroup</p></td>
<td><p>含群組語意的一般主體。不使用在 tblPrincipal 表格中。</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>SystemUser</p></td>
<td><p>常設聊天室伺服器 在內部使用的 Principal。</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>5</p></td>
<td><p>使用者</p></td>
<td><p>一般使用者。</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p>DC</p></td>
<td><p>Active Directory 網域服務 網域控制站。</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p>群組</p></td>
<td><p>Active Directory 安全性群組。</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>10</p></td>
<td><p>資料夾</p></td>
<td><p>Active Directory 容器或組織單位。</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[Lync Server 2013 中的 tblPrincipal](lync-server-2013-tblprincipal.md)

