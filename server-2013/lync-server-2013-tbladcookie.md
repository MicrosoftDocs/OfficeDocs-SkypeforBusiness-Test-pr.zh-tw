---
title: Lync Server 2013：tblADCookie
TOCTitle: tblADCookie
ms:assetid: 0a9102c4-47aa-40ea-8a0d-20e72ab09848
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558610(v=OCS.15)
ms:contentKeyID: 49290039
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblADCookie

 

_**上次修改主題的時間：** 2015-03-09_

tblADCookie 包含目前的輕量型目錄存取通訊協定 (LDAP) 同步處理 Cookie。

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
<td><p>受監控網域的主體 GUID。</p></td>
</tr>
<tr class="even">
<td><p>prinDCHost</p></td>
<td><p>nvarchar(255)</p></td>
<td><p>目前用於 Active Directory 網域服務 同步處理之網域控制站的完整網域名稱 (FQDN)。具有資訊值。</p></td>
</tr>
<tr class="odd">
<td><p>adcContent</p></td>
<td><p>影像 (二進位)</p></td>
<td><p>Active Directory 同步處理 Cookie。</p></td>
</tr>
<tr class="even">
<td><p>lastUpdated</p></td>
<td><p>datetime</p></td>
<td><p>含有列更新時間的時間戳記。</p></td>
</tr>
<tr class="odd">
<td><p>lockedUntil</p></td>
<td><p>datetime</p></td>
<td><p>鎖定列以進行變更的時間。這是軟體聯鎖機制的一部分，可確保一次僅有一個聊天服務會進行 Active Directory 同步處理。</p></td>
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
<th>欄位</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>prinGuid</p></td>
<td><p>主索引鍵。</p></td>
</tr>
<tr class="even">
<td><p>prinGuid</p></td>
<td><p>在 Principal.prinID 表格中查閱外部索引鍵。</p></td>
</tr>
</tbody>
</table>

