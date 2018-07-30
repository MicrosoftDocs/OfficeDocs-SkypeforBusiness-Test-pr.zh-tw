---
title: Lync Server 2013：回應群組的容量規劃
TOCTitle: 回應群組的容量規劃
ms:assetid: a2459a69-1f45-4f2f-bca5-d4f442708e44
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412754(v=OCS.15)
ms:contentKeyID: 49291853
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的回應群組的容量規劃

 

_**上次修改主題的時間：** 2015-03-09_

下表說明可供您作為容量規劃需求之基礎的 回應群組使用者模型。

> [!NOTE]  
> 下表中的數字假設您使用 16 kHz 的單聲道 16 位元 Wave (.wav) 檔做為所有回應群組音訊檔。如果您使用其他檔案格式 (例如 Windows Media Audio (.wma))，則數字可能有所不同。



> [!IMPORTANT]  
> 請記住，在災害復原容量規劃中，配對集區中的每一個集區都要能夠處理兩個集區中所有回應群組的工作負載。



### 回應群組使用者模型

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>計量單位</th>
<th>每個 Enterprise Edition 集區 (包含 8 部前端伺服器)</th>
<th>每個 Standard Edition Server</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>每秒來電數</p></td>
<td><p>16</p></td>
<td><p>2</p></td>
</tr>
<tr class="even">
<td><p>連線至 IVR 或 MoH 的並行通話數</p></td>
<td><p>480</p></td>
<td><p>60</p></td>
</tr>
<tr class="odd">
<td><p>並行匿名工作階段數 (不含 IM)</p></td>
<td><p>224</p></td>
<td><p>28</p></td>
</tr>
<tr class="even">
<td><p>並行匿名工作階段數 (包含 IM)</p></td>
<td><p>64</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p>作用中的代理程式 (正式和非正式)</p></td>
<td><p>1200</p></td>
<td><p>1200</p></td>
</tr>
<tr class="even">
<td><p>群組搜尋數目</p></td>
<td><p>400</p></td>
<td><p>400</p></td>
</tr>
<tr class="odd">
<td><p>IVR 群組數 (使用語音辨識)</p></td>
<td><p>200</p></td>
<td><p>200</p></td>
</tr>
</tbody>
</table>

