---
title: Lync Server 2013：tblSiopWhiteList
TOCTitle: tblSiopWhiteList
ms:assetid: 05fc1df4-32eb-4d46-9d1c-e0b607091142
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558607(v=OCS.15)
ms:contentKeyID: 49289975
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblSiopWhiteList

 

_**上次修改主題的時間：** 2015-03-09_

tblSiopWhiteList 是可與節點相關聯的註冊增益集清單。

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
<td><p>siopID</p></td>
<td><p>GUID，非 null</p></td>
<td><p>增益集的 GUID。</p></td>
</tr>
<tr class="even">
<td><p>siopName</p></td>
<td><p>nvarchar (50)，非 null</p></td>
<td><p>增益集的顯示名稱。</p></td>
</tr>
<tr class="odd">
<td><p>siopUrl</p></td>
<td><p>nvarchar (255)，非 null</p></td>
<td><p>增益集的 URL。</p></td>
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
<td><p>siopID</p></td>
<td><p>主索引鍵。</p></td>
</tr>
</tbody>
</table>

