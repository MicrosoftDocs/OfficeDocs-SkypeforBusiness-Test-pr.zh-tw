---
title: Lync Server 2013：tblPreference
TOCTitle: tblPreference
ms:assetid: f94eb128-f782-42ff-a568-ed3529573bc8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615052(v=OCS.15)
ms:contentKeyID: 49292876
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblPreference

 

_**上次修改主題的時間：** 2015-03-09_

tblPreference 包含使用者的用戶端喜好設定。通常是由比 Lync 2013 更舊版的用戶端使用。

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
<td><p>prefLabel</p></td>
<td><p>nvarchar (255)，非 null</p></td>
<td><p>格式如 &lt;使用者 SIP UIR&gt;|username.&lt;喜好設定集&gt; 的標籤。</p></td>
</tr>
<tr class="even">
<td><p>prefSeqID</p></td>
<td><p>int，非 null</p></td>
<td><p>設定版本的序號 (每個標籤各一個)。</p></td>
</tr>
<tr class="odd">
<td><p>prefContent</p></td>
<td><p>nvarchar (max)</p></td>
<td><p>編編的內容。</p></td>
</tr>
<tr class="even">
<td><p>lastModifiedBy</p></td>
<td><p>int，非 null</p></td>
<td><p>更新喜好設定之主體的 ID。</p></td>
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
<td><p>&lt;prefLabel, prefSeqID&gt;</p></td>
<td><p>主索引鍵。</p></td>
</tr>
</tbody>
</table>

