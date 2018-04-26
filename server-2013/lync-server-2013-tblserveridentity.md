---
title: Lync Server 2013：tblServerIdentity
TOCTitle: tblServerIdentity
ms:assetid: 5411c9bc-b0b3-41fc-8b7e-fa71cccd770b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558648(v=OCS.15)
ms:contentKeyID: 49290935
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblServerIdentity

 

_**上次修改主題的時間：** 2015-03-09_

tblServerIdentity 在 Persistent Chat Server 集區中包含作用中的聊天伺服器。

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
<td><p>serverID</p></td>
<td><p>int，非 null</p></td>
<td><p>伺服器識別碼。對應至 中央管理存放區的執行個體識別碼。</p></td>
</tr>
<tr class="even">
<td><p>serverAddress</p></td>
<td><p>nvarchar (256)，非 null</p></td>
<td><p>使用 Windows Communication Foundation 位址的伺服器位址。</p></td>
</tr>
<tr class="odd">
<td><p>serverLastPingTime</p></td>
<td><p>datetime</p></td>
<td><p>通道伺服器更新此列以證明其為執行中的最新時間。</p></td>
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
<td><p>serverID</p></td>
<td><p>主索引鍵。</p></td>
</tr>
</tbody>
</table>

