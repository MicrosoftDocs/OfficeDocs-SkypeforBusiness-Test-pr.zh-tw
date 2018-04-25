---
title: Lync Server 2013：Endpoint 表格
TOCTitle: Endpoint 表格
ms:assetid: 500f330d-4d7d-4e88-b1cc-fef9a9de6b5c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398327(v=OCS.15)
ms:contentKeyID: 49290902
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Endpoint 表格

 

_**上次修改主題的時間：** 2015-03-09_

Endpoint 表格是一種支援資料表，儲存資料庫中所記錄的工作階段之參與端點的資訊。表格中的每筆記錄代表一個端點。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>欄</strong></th>
<th><strong>資料類型</strong></th>
<th><strong>索引鍵/索引</strong></th>
<th><strong>詳細資料</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EndpointKey</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>用於識別此端點的唯一號碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>名稱</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>唯一</p></td>
<td><p>端點名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OS</strong></p></td>
<td><p>nvarchar(128)</p></td>
<td><p> </p></td>
<td><p>端點的作業系統 (OS)。</p></td>
</tr>
<tr class="even">
<td><p><strong>CPUName</strong></p></td>
<td><p>nvarchar(128)</p></td>
<td><p></p></td>
<td><p>端點的 CPU 名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CPUNumberOfCores</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>端點的 CPU 核心數。</p></td>
</tr>
<tr class="even">
<td><p><strong>CPUProcessorSpeed</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>端點的 CPU 處理器速度。</p></td>
</tr>
<tr class="odd">
<td><p><strong>VirtualizationFlag</strong></p></td>
<td><p>Tinyint</p></td>
<td><p></p></td>
<td><p>位元旗幟，指出系統是否在虛擬化環境中執行：</p>
<ul>
<li><p>0x0000 – 無</p></li>
<li><p>0x0001 – HyperV</p></li>
<li><p>0x0002 – VMWare</p></li>
<li><p>0x0004 – 虛擬電腦</p></li>
<li><p>0x0008 – Xen 電腦</p></li>
</ul></td>
</tr>
</tbody>
</table>

