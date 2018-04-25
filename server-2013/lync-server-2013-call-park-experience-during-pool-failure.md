---
title: Lync Server 2013：集區失敗期間的通話駐留體驗
TOCTitle: 集區失敗期間的通話駐留體驗
ms:assetid: f6303e69-8771-492a-9e8b-c3d7ba231309
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205383(v=OCS.15)
ms:contentKeyID: 49292833
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 集區失敗期間使用 Lync Server 2013 的通話駐留體驗

 

_**上次修改主題的時間：** 2015-03-09_

因不在規劃內的意外，導致無法使用 前端集區 時，會中斷已駐留但尚未擷取的通話。容錯移轉至備份集區期間，會將使用者重新導向至備份集區，並使其處於復原模式。在復原模式下，使用者無法駐留通話，但可保留與轉接通話。完成容錯移轉時，即可再次正常駐留與擷取通話。容錯回復期間，只要使用者處於復原模式，即無法駐留通話。

災難復原期間，屬於部分容錯移轉程序而重新導向至備份集區的使用者，會使用在備份集區部署的 通話駐留應用程式；因此這些使用者會使用在備份集區 通話駐留應用程式 中設定的通話駐留設定值。

下表摘述歷經災難復原階段的 通話駐留。

### 災難復原期間使用者的經驗

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>呼叫狀態</th>
<th>發生中斷時</th>
<th>容錯移轉期間</th>
<th>容錯回復期間</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>尚未駐留通話時</p></td>
<td><p>通話保持連線，但無法駐留。</p></td>
<td><ul>
<li><p>容錯移轉期間，使用者處於復原模式，無法駐留通話，但可保留與轉接通話。</p></li>
<li><p>完成容錯移轉時，即可駐留與擷取通話。</p></li>
</ul></td>
<td><ul>
<li><p>容錯回復期間，使用者處於復原模式，無法駐留通話，但可保留與轉接通話。</p></li>
<li><p>完成容錯回復時，即可駐留與擷取通話。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>通話已駐留，但尚未擷取</p></td>
<td><p>通話已中斷。</p></td>
<td><p>無此狀態的通話。</p></td>
<td><p>通話保持駐留。</p></td>
</tr>
<tr class="odd">
<td><p>已擷取通話。</p></td>
<td><p>通話保持連線。</p></td>
<td><p>通話保持連線。</p></td>
<td><p>通話保持連線。</p></td>
</tr>
</tbody>
</table>

