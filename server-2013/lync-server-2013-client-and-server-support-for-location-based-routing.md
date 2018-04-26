---
title: Lync Server 2013：位置基礎路由的用戶端和伺服器支援
TOCTitle: 位置基礎路由的用戶端和伺服器支援
ms:assetid: 26c2ca3d-026d-4dd7-94fa-15ebb4406953
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994024(v=OCS.15)
ms:contentKeyID: 52056073
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的位置基礎路由的用戶端和伺服器支援

 

_**上次修改主題的時間：** 2015-03-09_

位置基礎路由是由 Lync Server 執行。 Lync Server 能夠識別使用者將自企業網路內部連接的網站。由於遠端使用者位於企業網路之外，因此位置會被視為未知。

## Lync Server 支援

位置基礎路由需要於特定拓撲內所有 前端集區 和 Standard Edition 伺服器 上部署 Lync Server 2013 CU1。如果拓撲中特定 Lync 元件並未安裝 Lync Server 2013 CU1，就無法充分執行位置基礎路由限制。

下表顯示位置基礎路由支援的伺服器角色和版本組合。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>集區版本</th>
<th>中繼伺服器 版本</th>
<th>支援</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync Server 2013 累計更新 (2013 年 2 月)</p></td>
<td><p>Lync Server 2013 累計更新 (2013 年 2 月)</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2013 累計更新 (2013 年 2 月)</p></td>
<td><p>Lync Server 2013</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013 累計更新 (2013 年 2 月)</p></td>
<td><p>Lync Server 2010</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2013 累計更新 (2013 年 2 月)</p></td>
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p>任何</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2010</p></td>
<td><p>任何</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>任何</p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>


## Lync 用戶端支援

下表顯示位置基礎路由支援的用戶端。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端類型</th>
<th>支援</th>
<th>詳細資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 2013</p></td>
<td><p>是</p></td>
<td><p>包括 Lync 2013 累計更新 (2013 年 2 月)</p></td>
</tr>
<tr class="even">
<td><p>Lync 2010</p></td>
<td><p>是</p></td>
<td> </td>
</tr>
<tr class="odd">
<td><p>Office Communicator 2007 R2</p></td>
<td><p>否</p></td>
<td> </td>
</tr>
<tr class="even">
<td><p>Lync Phone Edition</p></td>
<td><p>是</p></td>
<td> </td>
</tr>
<tr class="odd">
<td><p>Lync Attendant</p></td>
<td><p>是</p></td>
<td> </td>
</tr>
<tr class="even">
<td><p>Lync for Windows 8</p></td>
<td><p>否</p></td>
<td> </td>
</tr>
<tr class="odd">
<td><p>Lync Mobile 2013</p></td>
<td><p>否</p></td>
<td><p>如果使用者啟用了位置基礎路由，則必須為 Lync Mobile 2013 用戶端停用 VoIP。</p></td>
</tr>
<tr class="even">
<td><p>Lync Mobile 2010</p></td>
<td><p>是</p></td>
<td> </td>
</tr>
</tbody>
</table>

  

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要為 Lync Mobile 2013 用戶端停用 VoIP，請為所有啟用了位置基礎路由的使用者指派已停用 IP 音訊/視訊設定的行動原則。如需有關行動原則的詳細資訊，請參閱＜ <a href="new-csmobilitypolicy.md">New-CsMobilityPolicy</a>＞。</td>
</tr>
</tbody>
</table>


## 請參閱

#### 其他資源

[在 Lync Server 2013 中規劃位置基礎路由](lync-server-2013-planning-for-location-based-routing.md)

