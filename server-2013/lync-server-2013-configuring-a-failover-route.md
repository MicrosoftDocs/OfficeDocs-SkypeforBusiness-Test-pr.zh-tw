---
title: Lync Server 2013：設定容錯移轉路由
TOCTitle: 設定容錯移轉路由
ms:assetid: 76e48df4-3b78-4fb7-b1f7-c1e604b81bad
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398581(v=OCS.15)
ms:contentKeyID: 49291362
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定容錯移轉路由

 

_**上次修改主題的時間：** 2015-03-09_

下列範例顯示系統管理員如何定義當 Dallas-GW1 因維修或其他緣故而無法使用時所要使用的容錯移轉路由。下表說明所需的設定變更。

### 表 1. 使用者原則

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>使用者原則</th>
<th>電話使用方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>預設通話原則</p></td>
<td><p>Local</p>
<p>GlobalPSTNHopoff</p></td>
</tr>
<tr class="even">
<td><p>Redmond 本地原則</p></td>
<td><p>RedmondLocal</p></td>
</tr>
<tr class="odd">
<td><p>Dallas 通話原則</p></td>
<td><p>DallasUsers</p>
<p>GlobalPSTNHopoff</p></td>
</tr>
</tbody>
</table>


### 表 2. 路由

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>路由名稱</th>
<th>號碼模式</th>
<th>電話使用方式</th>
<th>主幹</th>
<th>Gateway</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Redmond 本地路由</p></td>
<td><p>^\+1(425|206|253)(\d{7})$</p></td>
<td><p>Local</p>
<p>RedmondLocal</p></td>
<td><p>主幹1</p>
<p>主幹2</p></td>
<td><p>Red-GW1</p>
<p>Red-GW2</p></td>
</tr>
<tr class="even">
<td><p>Dallas 本地路由</p></td>
<td><p>^\+1(972|214|469)(\d{7})$</p></td>
<td><p>Local</p></td>
<td><p>主幹3</p></td>
<td><p>Dallas-GW1</p></td>
</tr>
<tr class="odd">
<td><p>全域路由</p></td>
<td><p>^\+?(\d*)$</p></td>
<td><p>GlobalPSTNHopoff</p></td>
<td><p>主幹1</p>
<p>主幹2</p>
<p>主幹3</p></td>
<td><p>Red-GW1</p>
<p>Red-GW2</p>
<p>Dallas-GW1</p></td>
</tr>
<tr class="even">
<td><p>Dallas 使用者路由</p></td>
<td><p>^\+?(\d*)$</p></td>
<td><p>DallasUsers</p></td>
<td><p>主幹3</p></td>
<td><p>Dallas-GW1</p></td>
</tr>
</tbody>
</table>


表 1 中，在「Dallas 通話原則」的「DallasUsers」電話使用方式後，將新增 GlobalPSTNHopoff 電話使用方式。如此可讓具有「Dallas 通話原則」的電話在無法使用 DallasUsers 電話使用方式的路由時，可以使用為 GlobalPSTNHopoff 電話使用方式所設定的路由。

