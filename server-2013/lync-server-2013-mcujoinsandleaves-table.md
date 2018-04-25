---
title: Lync Server 2013：McuJoinsAndLeaves 表格
TOCTitle: McuJoinsAndLeaves 表格
ms:assetid: 4e073366-0b5d-45b4-a3f6-d63dd5fd9f25
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398316(v=OCS.15)
ms:contentKeyID: 49290875
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 McuJoinsAndLeaves 表格

 

_**上次修改主題的時間：** 2015-03-09_

下表中的每筆記錄包含一組使用者加入或離開會議伺服器的通話詳細資訊。例如，如果使用者加入包含 Web 會議和音訊/視訊元素的會議，則會針對使用者加入 Web 會議建立一筆記錄，並針對使用者加入音訊/視訊會議建立另一筆記錄。


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
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>主要，外部</p></td>
<td><p>會議執行個體的時間。會與 <strong>SessionIdSeq</strong> 搭配使用，專門用於識別會議執行個體。如需詳細資訊，請參閱＜ <a href="lync-server-2013-conferences-table.md">Lync Server 2013 中的 Conferences 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要，外部</p></td>
<td><p>用於識別會議執行個體的識別碼。會與 <strong>SessionIdTime</strong> 搭配使用，專門用於識別會議執行個體。如需詳細資訊，請參閱＜ <a href="lync-server-2013-conferences-table.md">Lync Server 2013 中的 Conferences 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserId</strong></p></td>
<td><p>int</p></td>
<td><p>主要，外部</p></td>
<td><p>用於識別此使用者的唯一號碼。如需詳細資訊，請參閱＜ <a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>McuUserInstance</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>如果使用者一次登入多部電腦或裝置，McuUserInstance 會識別唯一的使用者/裝置組合。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsFromPstn</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>使用者是否從 PSTN 加入。</p></td>
</tr>
<tr class="even">
<td><p><strong>McuId</strong></p></td>
<td><p>int</p></td>
<td><p>主要，外部</p></td>
<td><p>用於識別此會議伺服器的唯一號碼。如需詳細資訊，請參閱 <a href="lync-server-2013-mcus-table.md">Lync Server 2013 中的 Mcus 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DialogSessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>外部</p></td>
<td><p>工作階段要求的時間，會與 <strong>SessionIdSeq</strong> 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱＜ <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>DialogSessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>識別工作階段的識別碼，其會與 <strong>SessionIdTime</strong> 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱 <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserJoinTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>這個使用者加入此會議伺服器的時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserLeaveTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>這個使用者離開此會議伺服器的時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientVerId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>用於指定用戶端軟體在會議中使用的版本號碼的識別碼。如需詳細資訊，請參閱 <a href="lync-server-2013-clientversions-table.md">Lync Server 2013 中的 ClientVersions 表格</a>。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
</tbody>
</table>

