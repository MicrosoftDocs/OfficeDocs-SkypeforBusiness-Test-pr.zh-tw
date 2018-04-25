---
title: Lync Server 2013：tblADUpdates
TOCTitle: tblADUpdates
ms:assetid: ba19fa16-4d2d-4635-ac32-f93e09469546
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615033(v=OCS.15)
ms:contentKeyID: 49292138
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblADUpdates

 

_**上次修改主題的時間：** 2015-03-09_

tblADUpdates 表格包含 Active Directory 同步處理後續步驟尚未處理的 Active Directory 網域服務 變更。

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
<td><p>prinGuid</p></td>
<td><p>GUID，非 null</p></td>
<td><p>有所變更之物件的主要 GUID。</p></td>
</tr>
<tr class="even">
<td><p>prinADPath</p></td>
<td><p>nvarchar (384)，非 null</p></td>
<td><p>物件的辨別名稱。</p></td>
</tr>
<tr class="odd">
<td><p>prinAttributesChanged</p></td>
<td><p>bit，非 null</p></td>
<td><p>如有任何一項物件屬性變更，即為 True。</p></td>
</tr>
<tr class="even">
<td><p>prinMembersChanged</p></td>
<td><p>bit，非 null</p></td>
<td><p>若成員資格有所變更，即為 True。</p></td>
</tr>
<tr class="odd">
<td><p>prinAffiliationsChanged</p></td>
<td><p>bit，非 null</p></td>
<td><p>未使用。</p></td>
</tr>
<tr class="even">
<td><p>prinDeleted</p></td>
<td><p>bit，非 null</p></td>
<td><p>若物件已被刪除，即為 True。</p></td>
</tr>
<tr class="odd">
<td><p>lastUpdated</p></td>
<td><p>datetime，非 null</p></td>
<td><p>插入列時的時間戳記。</p></td>
</tr>
</tbody>
</table>

