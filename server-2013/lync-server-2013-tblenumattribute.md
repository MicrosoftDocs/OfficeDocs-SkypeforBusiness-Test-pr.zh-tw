---
title: Lync Server 2013：tblEnumAttribute
TOCTitle: tblEnumAttribute
ms:assetid: 17f8b87e-36a6-4f6a-8630-7c76b61a7595
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558617(v=OCS.15)
ms:contentKeyID: 49290221
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblEnumAttribute

 

_**上次修改主題的時間：** 2015-03-09_

tblEnumAttribute 表格是一種硬式編碼的表格，其中含有節點表格中所用的可見度及行為屬性。

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
<td><p>attributeID</p></td>
<td><p>smallint，非 null</p></td>
<td><p>屬性的識別碼。</p></td>
</tr>
<tr class="even">
<td><p>attributeName</p></td>
<td><p>nvarchar (256)，非 null</p></td>
<td><p>屬性名稱。</p></td>
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
<td><p>attributeID</p></td>
<td><p>主索引鍵。</p></td>
</tr>
</tbody>
</table>


### 表格值

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>attributeID</th>
<th>attributeName</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>可見度。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>行為。</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[Lync Server 2013 中的 tblNode](lync-server-2013-tblnode.md)

