---
title: Lync Server 2013：ErrorDef 表格
TOCTitle: ErrorDef 表格
ms:assetid: 6acf3b86-da61-4923-9812-300db6f66dec
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398503(v=OCS.15)
ms:contentKeyID: 49291218
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 ErrorDef 表格

 

_**上次修改主題的時間：** 2015-03-09_

ErrorDef 表格儲存可能發生之每種錯誤類型的資訊。每筆記錄代表一種錯誤類型。


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
<td><p><strong>ErrorId</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>用來識別此類型錯誤的唯一識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>回應碼</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>與此錯誤相關聯的標準 SIP 回應碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MsDiagId</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Microsoft 診斷識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>CallTypeId</strong></p></td>
<td><p>int</p></td>
<td><p>外部</p></td>
<td><p>通話類型。請參閱＜ <a href="lync-server-2013-calltype-table.md">Lync Server 2013 中的 CallType 表格</a>＞以取得詳細資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RequestType</strong></p></td>
<td><p>varbinary(33)</p></td>
<td><p> </p></td>
<td><p>失敗之要求的類型。</p>
<p>使用此語法可將此資料轉換為文字格式：</p>
<p><code>cast(cast(RequestType as varbinary(max)) as varchar(max))</code></p></td>
</tr>
<tr class="even">
<td><p><strong>ContentType</strong></p></td>
<td><p>varbinary(257)</p></td>
<td><p> </p></td>
<td><p>失敗之要求的內容類型。</p>
<p>您可以使用以下語法將此資料轉換成文字格式：</p>
<p><code>cast(cast(ContentType as varbinary(max)) as varchar(max))</code></p></td>
</tr>
</tbody>
</table>

