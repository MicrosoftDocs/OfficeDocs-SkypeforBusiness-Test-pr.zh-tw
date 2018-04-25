---
title: Lync Server 2013：通話轉接和來電轉接
TOCTitle: 通話轉接和來電轉接
ms:assetid: 978610ec-63c7-4cf6-ad7a-9ef91559bf12
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994051(v=OCS.15)
ms:contentKeyID: 52056153
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的通話轉接和來電轉接

 

_**上次修改主題的時間：** 2015-03-09_

當涉及 PSTN 端點時，位置基礎路由會分析來電者的端點和通話或來電將要轉接到的端點位置 (亦即通話/來電轉接目標)。位置基礎路由會根據兩個端點的位置，判斷是否應轉接通話或來電。

下表說明某個 Lync 使用者與 PSTN 端點進行通話，且該 Lync 使用者將通話轉接給另一位 Lync 使用者的案例。視轉接受話者端點的網站位置而定，位置基礎路由會影響通話轉接或來電轉接的路由。

### 起始通話轉接或來電轉接

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>使用者起始通話轉接/來電轉接</th>
<th>目標端點位於使用者起始通話轉接或來電轉接的網站</th>
<th>目標端點並非位於使用者起始通話轉接或來電轉接的網站</th>
<th>目標端點位於未知網站或未啟用位置基礎路由的網站</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 使用者</p></td>
<td><p>允許來電轉接或通話轉接</p></td>
<td><p>不允許來電轉接或通話轉接</p></td>
<td><p>不允許來電轉接或通話轉接</p></td>
</tr>
</tbody>
</table>

  

例如：某個與 PSTN 端點進行通話的 Lync 使用者，將通話轉接給另一位位於相同網站的 Lync 使用者。在此情況下，會允許通話轉接。

下表說明某個 Lync 使用者與另一個 Lync 使用者進行通話，且其中一位使用者將通話轉接到 PSTN 端點的案例。視轉接通話的受話者位置而定，表中說明位置基礎路由會如何影響通話。

### 通話轉接或來電轉接到 PSTN 端點

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>通話轉接/來電轉接端點目標</th>
<th>位於相同網站的 Lync 使用者</th>
<th>位於不同網站的 Lync 使用者</th>
<th>一位或兩位 Lync 使用者位於未知網站或未啟用位置基礎路由的網站</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PSTN 端點</p></td>
<td><p>轉接受話者的網站語音路由原則允許來電轉接或通話轉接</p></td>
<td><p>轉接受話者的網站語音路由原則允許來電轉接或通話轉接</p></td>
<td><p>轉接受話者的語音原則僅允許透過未啟用位置基礎路由的主幹進行來電轉接或通話轉接</p></td>
</tr>
</tbody>
</table>

  
例如，某個 Lync 使用者與另一個位於相同網站的 Lync 使用者進行通話，並將通話轉接到 PSTN 端點，在此情況下會允許通話轉接。

## 請參閱

#### 其他資源

[Lync Server 2013 中的位置基礎路由案例](lync-server-2013-scenarios-for-location-based-routing.md)

