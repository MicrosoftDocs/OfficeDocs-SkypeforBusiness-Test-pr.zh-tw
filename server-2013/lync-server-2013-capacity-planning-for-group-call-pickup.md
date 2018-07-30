---
title: 群組來電接聽的容量規劃
TOCTitle: 群組來電接聽的容量規劃
ms:assetid: 0d654a19-6cf0-4118-903d-ec2c4e519253
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ984297(v=OCS.15)
ms:contentKeyID: 52056051
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 群組來電接聽的容量規劃

 

_**上次修改主題的時間：** 2015-03-09_

下表說明可供您作為容量規劃需求之基礎的群組來電接聽使用者模型。

> [!IMPORTANT]  
> 群組來電接聽的基礎為通話駐留應用程式。請記住，對於災害復原容量規劃而言，配對集區中的任一集區都應能處理配對集區中兩個集區的通話駐留服務工作負載，包括群組來電接聽。



### 群組來電接聽使用者模型

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>計量單位</th>
<th>每個前端集區 (包含 8 部前端伺服器)</th>
<th>每部 Standard Edition 伺服器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>每個群組的建議使用者數目</p></td>
<td><p>50</p></td>
<td><p>50</p></td>
</tr>
<tr class="even">
<td><p>建議的群組數目</p></td>
<td><p>500</p></td>
<td><p>60</p></td>
</tr>
<tr class="odd">
<td><p>每個集區中啟用群組來電接聽的使用者數目上限</p></td>
<td><p>25,000</p></td>
<td><p>3,000</p></td>
</tr>
<tr class="even">
<td><p>每個集區中所有啟用群組來電接聽之使用者的來電最大速率 (每分鐘)</p></td>
<td><p>500</p></td>
<td><p>60</p></td>
</tr>
<tr class="odd">
<td><p>每個集區中使用者利用群組來電接聽來擷取電話的最大速率 (每分鐘)</p></td>
<td><p>200</p></td>
<td><p>25</p></td>
</tr>
</tbody>
</table>


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>對於包含少於 8 部前端伺服器的前端集區，請以線性方式計算計量。例如，若前端集區包含一部前端伺服器，則最大負載的計算方式為表中所示值的 1/8。</p></li>
<li><p>只要不超過每個集區的使用者數目上限，就可以增加或減少每個群組的建議使用者數目以及群組數目。例如，Standard Edition 伺服器可以包含 120 個群組，每個群組 25 位使用者，因為啟用群組來電接聽的使用者數目仍在使用者模型上限之內 (亦即，120 個群組乘以 25 位使用者為 3,000 位使用者啟用群組來電接聽)。</p></li>
</ul></td>
</tr>
</tbody>
</table>

