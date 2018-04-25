---
title: Lync Server 2013：tblComplianceData
TOCTitle: tblComplianceData
ms:assetid: 05b28f9b-4aba-4b69-ba8d-2ceeb6cbfaac
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558606(v=OCS.15)
ms:contentKeyID: 49289968
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblComplianceData

 

_**上次修改主題的時間：** 2015-03-09_

tblComplianceData 包含法規相符性介面卡尚未處理的規範事件。

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
<td><p>cmplEventID</p></td>
<td><p>bigint，非 NULL</p></td>
<td><p>事件識別碼。</p></td>
</tr>
<tr class="even">
<td><p>entryDate</p></td>
<td><p>smalldatetime，非 null</p></td>
<td><p>插入時間 (若是 cmplType=9，則可能是未來很久以後，因為此項目在此情況下只是預留位置)。</p></td>
</tr>
<tr class="odd">
<td><p>cmplType</p></td>
<td><p>int，非 null</p></td>
<td><p>規範事件的類型：</p>
<ul>
<li><p>1: 聊天</p></li>
<li><p>2: 對話</p></li>
<li><p>3: 檔案下載</p></li>
<li><p>4: 檔案上傳</p></li>
<li><p>9: 暫時性檔案傳輸</p></li>
<li><p>10: 聊天刪除 (及取代)</p></li>
<li><p>11: 聊天清除</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>cmplTime</p></td>
<td><p>bigint，非 NULL</p></td>
<td><p>事件的時間戳記。</p></td>
</tr>
<tr class="odd">
<td><p>cmplChannelUri</p></td>
<td><p>nvarchar (255)，非 null</p></td>
<td><p>通道統一資源識別項 (URI)。</p></td>
</tr>
<tr class="even">
<td><p>cmplChatID</p></td>
<td><p>bigint</p></td>
<td><p>聊天識別碼 (對應至 tblChat.chatId 表格)。</p></td>
</tr>
<tr class="odd">
<td><p>cmplUserID</p></td>
<td><p>int，非 null</p></td>
<td><p>發佈者的主體識別碼 (對應至 tblPrincipal.prinID 表格)。</p></td>
</tr>
<tr class="even">
<td><p>cmplUserUri</p></td>
<td><p>nvarchar (255)，非 null</p></td>
<td><p>使用者 URI。</p></td>
</tr>
<tr class="odd">
<td><p>cmplMessage</p></td>
<td><p>nvarchar (max)</p></td>
<td><p>訊息 (編碼取決於 cmplType)。</p></td>
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
<td><p>cmplEventID</p></td>
<td><p>主索引鍵。</p></td>
</tr>
</tbody>
</table>

