---
title: Lync Server 2013 中的網域準備所進行的變更
TOCTitle: Lync Server 2013 中的網域準備所進行的變更
ms:assetid: 9191221e-6166-4c2b-837e-fa73d90fdf80
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398742(v=OCS.15)
ms:contentKeyID: 49291669
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的網域準備所進行的變更

 

_**上次修改主題的時間：** 2015-03-09_

下表列出網域準備作業在網域根目錄上建立的存取控制項目 (ACE)。除非特別註明，否則所有 ACE 都是繼承的。

### 新增到網域根目錄的 ACE

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>ACE</th>
<th>RTCUniversal-UserReadOnly-Group</th>
<th>RTCUniversal-ServerReadOnly-Group</th>
<th>RTCUniversal-UserAdmins</th>
<th>RTCHSUniversal-Services</th>
<th>Authenticated-Users</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>讀取容器 (非繼承的)</p></td>
<td><p><strong>是</strong></p></td>
<td><p><strong>是</strong></p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>讀取使用者屬性集 User-Account-Restrictions</p></td>
<td><p><strong>是</strong></p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>讀取使用者屬性集 Personal-Information</p></td>
<td><p><strong>是</strong></p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>讀取使用者屬性集 General-Information</p></td>
<td><p><strong>是</strong></p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>讀取使用者屬性集 Public-Information</p></td>
<td><p><strong>是</strong></p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>讀取使用者屬性集 RTCUserSearchProperty-Set</p></td>
<td><p><strong>是</strong></p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p><strong>是</strong></p></td>
</tr>
<tr class="odd">
<td><p>讀取使用者屬性集 RTCPropertySet</p></td>
<td><p><strong>是</strong></p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>寫入使用者屬性 Proxy-Addresses</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p><strong>是</strong></p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>寫入使用者屬性集 RTCUserSearchProperty-Set</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p><strong>是</strong></p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>寫入使用者屬性集 RTCPropertySet</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p><strong>是</strong></p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>讀取所有 Active Directory 物件的屬性集 DS-Replication-Get-Changes</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p><strong>是</strong></p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>


下表列出網域準備作業在三個內建容器中建立的 ACE：使用者、電腦和網域控制站。除非特別註明，否則所有 ACE 都是繼承的。

### 新增到內建容器的 ACE

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>ACE</th>
<th>RTCUniversal-UserReadOnly-Group</th>
<th>RTCUniversal-ServerReadOnly-Group</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>讀取容器 (非繼承的)</p></td>
<td><p><strong>是</strong></p></td>
<td><p><strong>是</strong></p></td>
</tr>
</tbody>
</table>

