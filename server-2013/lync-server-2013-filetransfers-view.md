---
title: FileTransfers 檢視
TOCTitle: FileTransfers 檢視
ms:assetid: e52c3ad0-152e-4a18-af1c-1aff0d205151
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721914(v=OCS.15)
ms:contentKeyID: 49890355
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# FileTransfers 檢視

 

_**上次修改主題的時間：** 2015-03-09_

FileTranfer 檢視存放了對等檔案傳輸工作階段的相關資訊。此檢視已於＜Microsoft Lync Server 2013＞介紹過。

> [!NOTE]  
> FileTransfers 檢視除了包含下列欄位，還包含＜<a href="lync-server-2013-sessiondetails-view.md">SessionDetails 檢視</a>＞的所有欄位。




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
<td><p><strong>FileName</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>傳輸檔案的名稱</p></td>
</tr>
<tr class="even">
<td><p><strong>Cookie</strong></p></td>
<td><p>nvarchar(128)</p></td>
<td><p>可用來識別與此訊息相關聯的每則後續訊息。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FileIdentity</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>傳輸同一檔名的檔案時，方便識別的唯一識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>接受</strong></p></td>
<td><p>bit</p></td>
<td><p>可為 TRUE 或 NULL。若為 TRUE，則「拒絕」和「取消」為 NULL。</p></td>
</tr>
<tr class="odd">
<td><p><strong>拒絕</strong></p></td>
<td><p>bit</p></td>
<td><p>可為 TRUE 或 NULL。若為 TRUE，則「接受」和「取消」為 NULL。</p></td>
</tr>
<tr class="even">
<td><p><strong>取消</strong></p></td>
<td><p>bit</p></td>
<td><p>可為 TRUE 或 NULL。若為 TRUE，則「接受」和「拒絕」為 NULL。</p></td>
</tr>
</tbody>
</table>

