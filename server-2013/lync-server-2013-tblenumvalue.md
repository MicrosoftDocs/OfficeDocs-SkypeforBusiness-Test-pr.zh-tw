---
title: Lync Server 2013：tblEnumValue
TOCTitle: tblEnumValue
ms:assetid: a33df20c-d19d-4f5c-b012-29dab8fb9200
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615025(v=OCS.15)
ms:contentKeyID: 49291883
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblEnumValue

 

_**上次修改主題的時間：** 2015-03-09_

tblEnumValue 是一種硬式編碼表格，其中包含節點表格中所用屬性的可見度和行為值。

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
<td><p>valueID</p></td>
<td><p>smallint，非 null</p></td>
<td><p>值的識別碼。</p></td>
</tr>
<tr class="even">
<td><p>attributeID</p></td>
<td><p>smallint，非 null</p></td>
<td><p>屬性的識別碼。</p></td>
</tr>
<tr class="odd">
<td><p>attributeValue</p></td>
<td><p>nvarchar (256)，非 null</p></td>
<td><p>值的名稱。</p></td>
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
<td><p>valueID</p></td>
<td><p>主索引鍵。</p></td>
</tr>
<tr class="even">
<td><p>attributeID</p></td>
<td><p>在 tblEnumAttribute.attributeID 表格中查閱外部索引鍵。</p></td>
</tr>
</tbody>
</table>


### 表格值

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>valueID</th>
<th>attributeID</th>
<th>attributeValue</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2</p></td>
<td><p>1</p></td>
<td><p>私人</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>1</p></td>
<td><p>範圍</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>2</p></td>
<td><p>一般</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>2</p></td>
<td><p>視聽中心</p></td>
</tr>
<tr class="odd">
<td><p>6</p></td>
<td><p>1</p></td>
<td><p>開放</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[Lync Server 2013 中的 tblNode](lync-server-2013-tblnode.md)

