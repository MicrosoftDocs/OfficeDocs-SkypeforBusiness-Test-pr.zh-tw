---
title: Lync Server 2013：tblPrincipalMeta
TOCTitle: tblPrincipalMeta
ms:assetid: 808490d4-7d6d-47a2-b8af-b5940d47073b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615009(v=OCS.15)
ms:contentKeyID: 49291479
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblPrincipalMeta

 

_**上次修改主題的時間：** 2015-03-09_

tblPrincipalMeta 表格包含必須從 Active Directory 網域服務 重新整理的主體。

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
<td><p>prinID</p></td>
<td><p>int，非 null</p></td>
<td><p>主體識別碼。</p></td>
</tr>
<tr class="even">
<td><p>prinAffiliationsDirty</p></td>
<td><p>位元，非 null</p></td>
<td><p>若主體關係必須重新整理，則為 True。</p></td>
</tr>
<tr class="odd">
<td><p>prinAttributesDirty</p></td>
<td><p>位元，非 null</p></td>
<td><p>若主體屬性必須重新整理，則為 True。</p></td>
</tr>
<tr class="even">
<td><p>prinDeleted</p></td>
<td><p>位元，非 null</p></td>
<td><p>若主體已刪除，則為 True。</p></td>
</tr>
<tr class="odd">
<td><p>tryCount</p></td>
<td><p>int</p></td>
<td><p>至今嘗試從 AD DS 重新整理主體的次數。</p></td>
</tr>
<tr class="even">
<td><p>lastTry</p></td>
<td><p>datetime</p></td>
<td><p>最近一次嘗試重新整理主體的時間戳記。若尚未重新整理過，可以是 null。</p></td>
</tr>
<tr class="odd">
<td><p>nextTry</p></td>
<td><p>datetime</p></td>
<td><p>排定下次重新整理時間戳記。若未排定之後的重新整理，可以是 null。</p></td>
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
<td><p>prinID</p></td>
<td><p>主索引鍵。</p></td>
</tr>
<tr class="even">
<td><p>prinID</p></td>
<td><p>在 tblPrincipal.prinID 表格中查閱外部索引鍵。</p></td>
</tr>
</tbody>
</table>

