---
title: Lync Server 2013：tblActivePeers
TOCTitle: tblActivePeers
ms:assetid: b50c3f4a-bab6-4cb9-b40e-016cf1a9c607
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615030(v=OCS.15)
ms:contentKeyID: 49292063
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblActivePeers

 

_**上次修改主題的時間：** 2015-03-09_

tblActivePeers 包含聊天服務之間目前的對等連線。

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
<td><p>aplServerID</p></td>
<td><p>int，非 null</p></td>
<td><p>張貼項目之伺服器的識別碼。</p></td>
</tr>
<tr class="even">
<td><p>aplPeerID</p></td>
<td><p>int，非 null</p></td>
<td><p>張貼伺服器所連線之對等伺服器的識別碼。</p></td>
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
<td><p>&lt;aplServerID、aplPeerID&gt;</p></td>
<td><p>主索引鍵。</p></td>
</tr>
<tr class="even">
<td><p>aplServerID</p></td>
<td><p>在 tblServerIdentity.serverID 表格中查閱外部索引鍵。</p></td>
</tr>
<tr class="odd">
<td><p>aplPeerID</p></td>
<td><p>在 tblServerIdentity.serverID 表格中查閱外部索引鍵。</p></td>
</tr>
</tbody>
</table>

