---
title: Lync Server 2013：ClientVersions 表格
TOCTitle: ClientVersions 表格
ms:assetid: 542316cf-a6db-4d52-ab28-8bf6d27a3b48
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398356(v=OCS.15)
ms:contentKeyID: 49290941
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 ClientVersions 表格

 

_**上次修改主題的時間：** 2015-03-09_

ClientVersions 表格是一種支援資料表，儲存資料庫中所記錄的工作階段之各種參與用戶端類型和版本清單。表格中的每筆記錄代表一個用戶端版本。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>資料類型</th>
<th>索引鍵/索引</th>
<th>詳細資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>VersionId</strong></p></td>
<td><p><strong>int</strong></p></td>
<td><p>主要</p></td>
<td><p>用於識別此用戶端類型及版本的唯一號碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>Version</strong></p></td>
<td><p><strong>nvarchar(256)</strong></p></td>
<td><p></p></td>
<td><p>版本名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientType</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>指出工作階段所使用的用戶端類型。如需詳細資訊，請參閱 <a href="lync-server-2013-useragentdef-table.md">Lync Server 2013 中的 UserAgentDef 表</a>。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
</tbody>
</table>

