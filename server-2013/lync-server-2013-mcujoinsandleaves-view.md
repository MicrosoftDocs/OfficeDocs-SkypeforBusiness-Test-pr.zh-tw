---
title: McuJoinsAndLeaves 檢視
TOCTitle: McuJoinsAndLeaves 檢視
ms:assetid: 6f00b8e7-b8b6-4657-ac5e-d8a571806ae2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688088(v=OCS.15)
ms:contentKeyID: 49890110
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# McuJoinsAndLeaves 檢視

 

_**上次修改主題的時間：** 2015-03-09_

McuJoinsAndLeaves 檢視會儲存使用者加入或離開一個會議伺服器的相關資訊。這個檢視中的每筆記錄都包含一組使用者加入或離開會議伺服器的通話詳細資料。這個檢視是由 Microsoft Lync Server 2013 所引進。


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
<td><p>日期時間</p></td>
<td><p>會議執行個體的時間。會與 SessionIdSeq 搭配使用，專門用於識別會議執行個體。如需詳細資訊，請參閱＜<a href="lync-server-2013-conferences-table.md">Lync Server 2013 中的 Conferences 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>用於辨識執行個體的 ID 號碼。會與 SessionIDTime 搭配使用，專門用於識別會議執行個體。如需詳細資訊，請參閱＜<a href="lync-server-2013-conferences-table.md">Lync Server 2013 中的 Conferences 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>McuUri</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>使用者連線至會議伺服器的 URI。</p></td>
</tr>
<tr class="even">
<td><p><strong>McuUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>使用者連線至會議伺服器的 URI。如需詳細資訊，請參閱 <a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>擷取會議伺服器加入/離開資訊之使用者的 URI 。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>擷取會議伺服器加入/離開資訊之使用者的 URI 類型。如需詳細資訊，請參閱 <a href="lync-server-2013-uritypes-table.md">Lync Server 2013 中的 UriTypes 表格</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserTenant</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>擷取會議伺服器加入/離開資訊之使用者的租用戶。如需詳細資訊，請參閱＜<a href="lync-server-2013-tenants-table.md">Lync Server 2013 中的 Tenants 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserClientVersion</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>擷取會議伺服器加入/離開資訊之使用者所使用的用戶端版本。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserClientType</strong></p></td>
<td><p>int</p></td>
<td><p>擷取會議伺服器加入/離開資訊之使用者所使用的用戶端。如需詳細資訊，請參閱 <a href="lync-server-2013-useragentdef-table.md">Lync Server 2013 中的 UserAgentDef 表</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserClientCategory</strong></p></td>
<td><p>nvarchar(64)</p></td>
<td><p>擷取會議伺服器加入/離開資訊之使用者所使用的用戶端類別名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>McuUserInstance</strong></p></td>
<td><p>int</p></td>
<td><p>唯一識別使用者同時登入多個裝置的使用者/裝置組合。</p></td>
</tr>
<tr class="even">
<td><p><strong>IsUserFromPstn</strong></p></td>
<td><p>位元</p></td>
<td><p>位元表示使用者是否為內部使用者。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DialogSessionIdTime</strong></p></td>
<td><p>日期時間</p></td>
<td><p>工作階段要求的時間。與 SessionIdSeq 搭配使用，以唯一識別工作階段。如需詳細資訊，請參閱＜<a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>DialogSessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>識別工作階段的 ID 號碼。與 SessionIdTime 搭配使用，以唯一識別工作階段。如需詳細資訊，請參閱＜<a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DialogId</strong></p></td>
<td><p>varchar(775)</p></td>
<td><p>工作階段 SIP 對話方塊 ID。格式為：dialog;from-tag;to-tag。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserJoinTime</strong></p></td>
<td><p>日期時間</p></td>
<td><p>使用者加入會議伺服器的時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserLeaveTime</strong></p></td>
<td><p>日期時間</p></td>
<td><p>使用者離開會議伺服器的時間。</p></td>
</tr>
</tbody>
</table>

