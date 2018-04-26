---
title: FocusJoinsAndLeaves 檢視
TOCTitle: FocusJoinsAndLeaves 檢視
ms:assetid: 226460ef-766f-4d61-80cb-f332b65a210d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687992(v=OCS.15)
ms:contentKeyID: 49889976
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# FocusJoinsAndLeaves 檢視

 

_**上次修改主題的時間：** 2015-03-09_

FocusJoinsAndLeaves 檢視可儲存會議的加入和離開相關資訊。每次有使用者加入和離開某場會議時，此檢視中的該場會議都會有一筆撰寫記錄來表示。Microsoft Lync Server 2013 中即引入了此檢視。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>資料類型</th>
<th>詳細資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>會議執行個體的時間，其會與 SessionIdSeq 搭配使用，專門用於識別會議執行個體。如需詳細資訊，請參閱＜<a href="lync-server-2013-conferences-table.md">Lync Server 2013 中的 Conferences 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>識別會議執行個體的識別碼，其會與 SessionIdTime 搭配使用，專門用於識別會議執行個體。如需詳細資訊，請參閱＜<a href="lync-server-2013-conferences-table.md">Lync Server 2013 中的 Conferences 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>已擷取其加入/離開會議資訊之使用者的 URI。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>已擷取其加入/離開會議資訊之使用者的 URI 類型。如需詳細資訊，請參閱＜<a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserTenant</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>已擷取其加入/離開會議資訊之使用者的租用戶。如需詳細資訊，請參閱＜<a href="lync-server-2013-tenants-table.md">Lync Server 2013 中的 Tenants 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserEndpointId</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>已擷取其加入/離開會議資訊之使用者的唯一識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserClientVersion</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>已擷取其加入/離開會議資訊之使用者所用的用戶端版本。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserClientType</strong></p></td>
<td><p>int</p></td>
<td><p>已擷取其加入/離開會議資訊之使用者所用的用戶端。如需詳細資訊，請參閱＜<a href="lync-server-2013-useragentdef-table.md">Lync Server 2013 中的 UserAgentDef 表</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserClientCategory</strong></p></td>
<td><p>nvarchar(64)</p></td>
<td><p>已擷取其加入/離開會議資訊之使用者所用的用戶端類別名稱。</p></td>
</tr>
<tr class="even">
<td><p><strong>FocusUserInstance</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p><strong>IsuserInternal</strong></p></td>
<td><p>bit</p></td>
<td><p>代表使用者是否為內部使用者的位元。</p></td>
</tr>
<tr class="even">
<td><p><strong>DialogSessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>工作階段要求的時間，其會與 SessionIdSeq 搭配使用，專門用於識別工作階段。如需詳細資訊，請參閱＜<a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DialogSessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>若使用者同時登入多部電腦或裝置，會使用 UserInstance 專門識別使用者/裝置的組合。</p></td>
</tr>
<tr class="even">
<td><p><strong>DialogId</strong></p></td>
<td><p>varchar(775)</p></td>
<td><p>工作階段的 SIP 對話方塊識別碼，格式為：dialog;from-tag;to-tag。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserJoinTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>使用者加入會議的時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserLeaveTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>使用者離開會議的時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserRole</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>此使用者在會議中的角色，例如簡報者或是出席者。</p></td>
</tr>
</tbody>
</table>

