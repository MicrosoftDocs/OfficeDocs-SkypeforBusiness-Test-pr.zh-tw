---
title: Lync Server 2013：通話駐留的容量規劃
TOCTitle: 通話駐留的容量規劃
ms:assetid: 75520310-760a-4b1b-bcc1-4d724d13f87a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg416493(v=OCS.15)
ms:contentKeyID: 49291351
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中通話駐留的容量規劃

 

_**上次修改主題的時間：** 2015-03-09_

下表說明可供您作為容量規劃需求之基礎的 通話駐留使用者模型。

> [!IMPORTANT]  
> 請記住，針對災害復原處理能力規劃，已配對集區的每個集區都應能夠在兩個集區中處理 通話駐留服務的工作負載。



### 通話駐留使用者模型

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>計量單位</th>
<th>每個 前端集區 (包含 8 部前端伺服器)</th>
<th>每個 Standard Edition 伺服器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>駐留率</p></td>
<td><p>每分鐘 8 個</p></td>
<td><p>每分鐘 1 個</p></td>
</tr>
<tr class="even">
<td><p>擷取駐留通話率</p></td>
<td><p>每分鐘 8 個</p></td>
<td><p>每分鐘 1 個</p></td>
</tr>
<tr class="odd">
<td><p>平均駐留持續時間</p></td>
<td><p>60 秒</p></td>
<td><p>60 秒</p></td>
</tr>
</tbody>
</table>

