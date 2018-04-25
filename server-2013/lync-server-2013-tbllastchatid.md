---
title: Lync Server 2013：tblLastChatId
TOCTitle: tblLastChatId
ms:assetid: 17a4ffbe-cca9-4ec5-ae46-38a15274889a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558616(v=OCS.15)
ms:contentKeyID: 49290214
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblLastChatId

 

_**上次修改主題的時間：** 2015-03-09_

tblLastChatId 表格包含為每個使用者產生 (且用於 tblChat 表格) 的最後一個交談 ID。

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
<td><p>nodeID</p></td>
<td><p>int，非 null</p></td>
<td><p>節點識別碼 (僅聊天室類型)。</p></td>
</tr>
<tr class="even">
<td><p>lastChatID</p></td>
<td><p>bigint，非 NULL</p></td>
<td><p>最後一個使用的交談 ID。</p></td>
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
<td><p>&lt;nodeID, lastChatID&gt;</p></td>
<td><p>主索引鍵 (處理時僅有 nodeID 已足夠)。</p></td>
</tr>
<tr class="even">
<td><p>nodeID</p></td>
<td><p>在 tblNode.nodeID 表格中查閱外部索引鍵。</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[Lync Server 2013 中的 tblChat](lync-server-2013-tblchat.md)

