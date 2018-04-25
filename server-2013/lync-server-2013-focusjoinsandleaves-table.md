---
title: Lync Server 2013：FocusJoinsAndLeaves 表格
TOCTitle: FocusJoinsAndLeaves 表格
ms:assetid: e6f0212c-67e9-4061-8720-d0296e855991
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399026(v=OCS.15)
ms:contentKeyID: 49292646
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 FocusJoinsAndLeaves 表格

 

_**上次修改主題的時間：** 2015-03-09_

此表格中的每筆記錄都包含一位使用者加入和離開某會議的相關 CDR 資訊。此表格中的每個會議會在每次有使用者加入和離開會議，以一筆記錄表示。


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
<td><p><strong>DialogSessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>主要，外部</p></td>
<td><p>工作階段要求的時間，會與 <strong>SessionIdSeq</strong> 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱＜ <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>DialogSessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要，外部</p></td>
<td><p>識別工作階段的識別碼，會與 <strong>SessionIdTime</strong> 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱＜ <a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>用於識別此使用者的唯一號碼。參考來源： <a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>FocusUserInstance</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>若使用者同時登入多部電腦或裝置，會使用 <strong>UserInstance</strong> 專門識別使用者/裝置的組合。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsUserInternal</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>使用者是否從內部登入。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserRole</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>此使用者在會議中的角色，例如簡報者或是出席者。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserJoinTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>此使用者加入會議的時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserLeaveTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>此使用者離開會議的時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientVerId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>使用者用戶端軟體的版本，請參閱＜ <a href="lync-server-2013-clientversions-table.md">Lync Server 2013 中的 ClientVersions 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserEndpointId</strong></p></td>
<td><p>uniqueIdentifier</p></td>
<td><p></p></td>
<td><p>會議中所用端點的全域唯一識別碼 (GUID)。</p>
<p>此部分已於＜ Microsoft Lync Server 2013＞介紹過。</p></td>
</tr>
</tbody>
</table>

