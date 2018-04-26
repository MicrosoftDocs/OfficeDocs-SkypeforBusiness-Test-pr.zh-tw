---
title: Lync Server 2013：tblAdminLock
TOCTitle: tblAdminLock
ms:assetid: 785a43c0-6892-474c-821c-fa9cdbeb99d8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558665(v=OCS.15)
ms:contentKeyID: 49291383
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblAdminLock

 

_**上次修改主題的時間：** 2015-03-09_

tblAdminLock 表格包含執行某些系統管理員命令所需的系統管理員鎖定。

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
<td><p>lockExpiresTime</p></td>
<td><p>日期時間，非 null</p></td>
<td><p>鎖定到期的日期和時間。擁有者可定期延長這個值。</p></td>
</tr>
<tr class="even">
<td><p>lockServerID</p></td>
<td><p>int，非 null</p></td>
<td><p>掌握鎖定之伺服器的識別碼。</p></td>
</tr>
<tr class="odd">
<td><p>lockActorID</p></td>
<td><p>int，非 null</p></td>
<td><p>掌握鎖定之主體的識別碼。</p></td>
</tr>
</tbody>
</table>

