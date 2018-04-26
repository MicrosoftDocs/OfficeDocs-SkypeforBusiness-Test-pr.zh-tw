---
title: Lync Server 2013：撥出電話
TOCTitle: 撥出電話
ms:assetid: 885ffe6f-cd51-4f21-8d4f-a1ff8d818858
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994049(v=OCS.15)
ms:contentKeyID: 52056164
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中撥出電話

 

_**上次修改主題的時間：** 2015-03-09_

啟用位置基礎路由之使用者的輸出通話路由，會受使用者端點的網路位置影響。下表說明位置基礎路由如何取決於來電者的端點位置對輸出通話路由產生影響。

### 來電者撥打輸出通話給 PSTN

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>使用者端點位於啟用位置基礎路由的網站</th>
<th>使用者端點位於未知網站或未啟用位置基礎路由的網站</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>輸出通話授權</p></td>
<td><p>通話會根據使用者的語音原則獲得授權</p></td>
<td><p>通話會根據使用者的語音原則獲得授權</p></td>
</tr>
<tr class="even">
<td><p>輸出通話路由</p></td>
<td><p>通話會根據網站的語音路由原則路由傳送</p></td>
<td><p>通話會根據使用者的語音原則且僅透過未啟用位置基礎路由的主幹 (如果有的話) 路由傳送</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 其他資源

[Lync Server 2013 中的位置基礎路由案例](lync-server-2013-scenarios-for-location-based-routing.md)

