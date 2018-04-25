---
title: Lync Server 2013：tblChat
TOCTitle: tblChat
ms:assetid: b7fcf1b4-7a3f-4585-a6d9-95e7f030c7dc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615031(v=OCS.15)
ms:contentKeyID: 49292099
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblChat

 

_**上次修改主題的時間：** 2015-03-09_

tblChat 包含所有的聊天訊息。

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
<td><p>channelId</p></td>
<td><p>int，非 null</p></td>
<td><p>節點識別碼。</p></td>
</tr>
<tr class="even">
<td><p>chatId</p></td>
<td><p>bigint，非 NULL</p></td>
<td><p>由 tblLastChatId 表格產生的唯一序號 (每個節點識別碼)，可以定義聊天室的順序。</p></td>
</tr>
<tr class="odd">
<td><p>chatDate</p></td>
<td><p>bigint，非 NULL</p></td>
<td><p>聊天訊息的時間戳記。</p></td>
</tr>
<tr class="even">
<td><p>userId</p></td>
<td><p>int，非 null</p></td>
<td><p>張貼者的主要識別碼。</p></td>
</tr>
<tr class="odd">
<td><p>isAlert</p></td>
<td><p>位元，非 null</p></td>
<td><p>當訊息為警告訊息時為 True。反之即為 False。</p></td>
</tr>
<tr class="even">
<td><p>content</p></td>
<td><p>nvarchar (max)，非 null</p></td>
<td><p>聊天內容 (純文字版本)。內容通常為純文字，但下列項目除外：</p>
<ul>
<li><p>以 ma-filelink: links 表示的檔案。</p></li>
<li><p>以 HTML 元素表示 (雖然內容的類型不是 HTML) 的連結。</p></li>
<li><p>以 &quot;[STORY]....&quot; 類似格式編碼的本文。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>rtf</p></td>
<td><p>varchar(max)</p></td>
<td><p>聊天內容 (RTF 版本)。如果用戶端不提供，可能為 Null。</p></td>
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
<td><p>&lt;通道識別碼，聊天識別碼&gt;</p></td>
<td><p>主索引鍵。</p></td>
</tr>
</tbody>
</table>

