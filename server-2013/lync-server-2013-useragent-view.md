---
title: UserAgent 檢視
TOCTitle: UserAgent 檢視
ms:assetid: b986f76f-f16e-4e5e-96cb-6e8f7f9b42ee
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721862(v=OCS.15)
ms:contentKeyID: 49890279
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# UserAgent 檢視

 

_**上次修改主題的時間：** 2015-03-09_

UserAgent 檢視儲存資料庫中有記錄之工作階段相關的使用者代理程式資訊。此檢視已於 Microsoft Lync Server 2013 引進使用。


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
<td><p>UserAgentKey</p></td>
<td><p>int</p></td>
<td><p>識別此使用者代理程式且不重複的號碼。</p></td>
</tr>
<tr class="even">
<td><p>UserAgent</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>使用者代理程式字串。</p></td>
</tr>
<tr class="odd">
<td><p>UAType</p></td>
<td><p>smallint</p></td>
<td><p>使用者代理程式類型。如需詳細資訊，請參閱＜<a href="lync-server-2013-useragent-table.md">Lync Server 2013 中的 UserAgent 表格</a>＞。</p></td>
</tr>
<tr class="even">
<td><p>UACategory</p></td>
<td><p>nvarchar(64)</p></td>
<td><p>使用者代理程式所屬的類別。例如，使用者代理程式 Conferencing_Attendant_1.0 屬於 UACategory CAA。</p></td>
</tr>
</tbody>
</table>

