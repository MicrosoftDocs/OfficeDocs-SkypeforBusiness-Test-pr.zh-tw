---
title: Lync Server 2013：來電
TOCTitle: 來電
ms:assetid: 65b9c1b4-6af7-4527-8c33-22c4442bd209
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994038(v=OCS.15)
ms:contentKeyID: 52056121
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的來電

 

_**上次修改主題的時間：** 2015-03-09_

給啟用位置基礎路由之使用者的傳入通話路由，會視使用者的端點位置而定。傳入通話的路由會於下列方面受到影響。如果撥打給使用者的傳入通話是撥到啟用位置基礎路由之網站上的端點，且端點位於 PSTN 閘道所在的相同網站，則通話將會路由傳送。如果撥打給使用者的傳入通話是撥到啟用位置基礎路由之網站上的端點，且端點位於與 PSTN 閘道不同的網站，則通話將不會路由傳送。當使用者的端點並不在傳入通話之 PSTN 閘道所在的相同網站上時，傳入通話將會直接路由傳送到使用者的語音信箱，且將會傳送未接電話通知給受話方。

啟用位置基礎路由之使用者的來電轉接設定將會繼續執行，然而，轉接的來電將會受到使用者的位置基礎路由限制。

下表說明根據受話者的端點位置，位置基礎路由會對輸入通話的路由有何影響。PSTN 閘道網站已啟用位置基礎路由，且位置基礎路由只允許將 PSTN 通話路由到位於相同網站內的端點。

### 受話者收到來自 PSTN 的輸入通話

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>受話者的端點位於 PSTN 閘道所在之網站</th>
<th>受話者的端點並不在 PSTN 閘道所在之網站</th>
<th>受話者的端點位於未知網站或未啟用位置基礎路由的網站</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>輸入 PSTN 通話的路由</p></td>
<td><p>傳入通話會路由傳送到受話者的端點</p></td>
<td><p>傳入通話不會路由傳送到受話者的端點</p></td>
<td><p>傳入通話不會路由傳送到受話者的端點</p></td>
</tr>
</tbody>
</table>

  

## 請參閱

#### 其他資源

[Lync Server 2013 中的位置基礎路由案例](lync-server-2013-scenarios-for-location-based-routing.md)

