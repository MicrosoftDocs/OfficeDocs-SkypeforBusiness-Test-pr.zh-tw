---
title: Lync Server 2013：tblComplianceParticipant
TOCTitle: tblComplianceParticipant
ms:assetid: 5d7e0dea-74f7-46d1-badf-b94abc8f066d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558655(v=OCS.15)
ms:contentKeyID: 49291056
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblComplianceParticipant

 

_**上次修改主題的時間：** 2015-03-09_

tblComplianceParticipant 包含每個通道和每部伺服器的目前參與者。

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
<td><p>channelUri</p></td>
<td><p>nvarchar (255)，非 null</p></td>
<td><p>通道統一資源識別項 (URI)。</p></td>
</tr>
<tr class="even">
<td><p>userId</p></td>
<td><p>int，非 null</p></td>
<td><p>參與者的主體識別碼 (對應至 tblPrincipal.prinID 表格)。</p></td>
</tr>
<tr class="odd">
<td><p>joinedAt</p></td>
<td><p>bigint，非 NULL</p></td>
<td><p>加入活動的時間戳記。</p></td>
</tr>
<tr class="even">
<td><p>partedAt</p></td>
<td><p>bigint</p></td>
<td><p>如果參與者仍加入，則為 Null。如果不是 Null，則是通道離開事件的時間戳記。</p>
<p>當所有轉譯器處理事件時，這些項目最後都會移除。</p></td>
</tr>
<tr class="odd">
<td><p>userUri</p></td>
<td><p>nvarchar (255)，非 null</p></td>
<td><p>使用者 URI。</p></td>
</tr>
<tr class="even">
<td><p>serverID</p></td>
<td><p>int</p></td>
<td><p>伺服器識別碼 (如 tblServerIdentity.serverID 表格中所示)。</p></td>
</tr>
<tr class="odd">
<td><p>sessionId</p></td>
<td><p>bigint</p></td>
<td><p>伺服器工作階段。這是聊天服務每次啟動時，所產生的隨機號碼。在識別孤立的參與者時，可使用此號碼來區別工作階段。</p></td>
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
<td><p>&lt;channelUri, userId, joinedAt&gt;</p></td>
<td><p>主索引鍵。</p></td>
</tr>
</tbody>
</table>

