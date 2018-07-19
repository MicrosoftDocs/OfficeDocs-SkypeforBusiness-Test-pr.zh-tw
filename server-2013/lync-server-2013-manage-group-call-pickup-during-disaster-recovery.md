---
title: 管理災害復原期間的群組來電接聽
TOCTitle: 管理災害復原期間的群組來電接聽
ms:assetid: 2d32f19f-c649-4a72-a4fb-edd338e3a7cc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945618(v=OCS.15)
ms:contentKeyID: 52056079
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 管理災害復原期間的群組來電接聽

 

_**上次修改主題的時間：** 2015-03-09_

當前端集區因為未預先計畫的事件而變成無法使用時，服務就會容錯移轉至備份集區。容錯移轉至備份集區期間，系統會將使用者重新導向至備份集區，並使其處於復原模式。在復原模式下，使用者無法接聽其他使用者的電話，也無法把他自己的電話讓其他使用者接聽。容錯移轉完成後，使用者就可以像往常一樣再次使用群組來電接聽。

容錯回復至主要集區期間，系統會將使用者重新導向至主要集區，並使其再次處於恢復模式。直到使用者離開恢復模式之後，群組來電接聽功能才能再次使用。

本節會討論災害復原期間對群組來電接聽的某些考量，同時說明使用者的體驗。

## 災害復原期間的群組來電接聽考量

在災害復原期間，因為容錯移轉程序而重新導向至備份集區的使用者，會使用在備份集區中執行的通話駐留應用程式來使用電話接聽群組號碼。因此，若要在災害復原期間支援群組來電接聽，就必須在主要集區與備份集區兩者中都部署並啟用通話駐留應用程式。

在容錯移轉至備份集區的程序完成後，通話駐留範圍表中的群組來電接聽號碼範圍必須重新導向至備份集區。而在容錯回復至主要集區的程序完成後，號碼範圍就必須重新導向回到主要集區。若要重新導向群組來電接聽範圍，請使用 **Set-CsCallParkOrbit** Cmdlet。

如果您部署具備不同完整網域名稱 (FQDN) 的新集區以取代主要集區，則必須將所有原先與主要集區相關聯之群組來電接聽號碼範圍重新指派給新集區的 FQDN。若要將號碼範圍重新指派給新集區，可使用 **Set-CsCallParkOrbit** Cmdlet。如需 **Set-CsCallParkOrbit** Cmdlet 的詳細資訊，請參閱＜[Set-CsCallParkOrbit](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCallParkOrbit)＞。

## 集區失敗期間的群組來電接聽體驗

下表摘述在整個災害復原階段期間的群組來電接聽體驗。

### 災害復原期間的使用者體驗

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>通話狀態</th>
<th>容錯移轉至備份集區</th>
<th>容錯回復至主要集區</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>新通話</p></td>
<td><p><strong>在容錯移轉程序期間︰</strong></p>
<ul>
<li><p>在恢復模式下的使用者無法使用群組來電接聽</p></li>
</ul>
<p><strong>在容錯移轉完成後︰</strong></p>
<ul>
<li><p>當使用者離開恢復模式，且群組來電接聽號碼範圍重新導向至備份集區之後，群組來電接聽即可使用</p></li>
</ul></td>
<td><p><strong>在容錯回復程序期間︰</strong></p>
<ul>
<li><p>在恢復模式下的使用者無法使用群組來電接聽</p></li>
</ul>
<p><strong>在容錯回復完成後︰</strong></p>
<ul>
<li><p>當使用者離開恢復模式，且群組來電接聽號碼範圍重新導向回到主要集區之後，群組來電接聽即可使用</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>群組來電接聽佇列中的通話</p></td>
<td><p><strong>在容錯移轉程序期間︰</strong></p>
<ul>
<li><p>佇列中的通話無法透過群組來電接聽來接聽。</p></li>
</ul>
<p><strong>在容錯移轉完成後︰</strong></p>
<ul>
<li><p>無此狀態的通話</p></li>
</ul></td>
<td><p><strong>在容錯回復程序期間︰</strong></p>
<ul>
<li><p>佇列中的通話無法透過群組來電接聽來接聽。</p></li>
</ul>
<p><strong>在容錯回復完成後︰</strong></p>
<ul>
<li><p>佇列中的通話無法透過群組來電接聽來接聽。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>建立的通話</p></td>
<td><p><strong>在容錯移轉程序期間︰</strong></p>
<ul>
<li><p>通話保持接通的狀態</p></li>
</ul>
<p><strong>在容錯移轉完成後︰</strong></p>
<ul>
<li><p>通話保持接通的狀態</p></li>
</ul></td>
<td><p><strong>在容錯回復程序期間︰</strong></p>
<ul>
<li><p>通話保持接通的狀態</p></li>
</ul>
<p><strong>在容錯回復完成後︰</strong></p>
<ul>
<li><p>通話保持接通的狀態</p></li>
</ul></td>
</tr>
</tbody>
</table>

