---
title: Lync Server 2013：Dialogs 表格
TOCTitle: Dialogs 表格
ms:assetid: 487a430b-af66-4ea6-b28e-4e33cfdb7f9e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425954(v=OCS.15)
ms:contentKeyID: 49290802
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Dialogs 表格

 

_**上次修改主題的時間：** 2015-03-09_

Dialogs 表格是一種支援資料表，可儲存點對點工作階段的 DialogID 資訊。


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
<td><p>主要</p></td>
<td><p>工作階段要求的時間；其會與 SessionIDSeq 搭配使用，專門用於識別工作階段。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>識別工作階段的識別碼。其會與 SessionIDTime 搭配使用，專門用於識別工作階段。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ExternalChecksum</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>ExternalID 的總和檢查碼。此欄位可用來增加資料庫搜尋的速度。</p></td>
</tr>
<tr class="even">
<td><p><strong>ExternalId</strong></p></td>
<td><p>varbinary(775)</p></td>
<td><p> </p></td>
<td><p>SIP 對話方塊識別碼，儲存成二進位。二進位的格式為</p>
<p>dialog;from-tag;to-tag</p>
<p>使用此語法可將此資料轉換為文字格式：</p>
<p><code>cast(cast(ExternalId as varbinary(max)) as varchar(max))</code></p></td>
</tr>
</tbody>
</table>

