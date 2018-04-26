---
title: Lync Server 2013：同時響鈴
TOCTitle: 同時響鈴
ms:assetid: df02f919-4d50-4832-9300-6c51f8b4fc56
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994079(v=OCS.15)
ms:contentKeyID: 52056236
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的同時響鈴

 

_**上次修改主題的時間：** 2015-03-09_

當受話方啟用了同時響鈴時，位置基礎路由會分析來電者的位置和受話方的端點，以判斷是否應路由傳送通話。

下表說明某個使用者設定了同時響鈴，且同時響鈴目標為位於相同網站、不同網站或未知網站之使用者的情況。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>傳入 PSTN 通話對象</th>
<th>位於與受話者相同的網站</th>
<th>位於與受話者不同的網站</th>
<th>位於未知網站或未啟用位置基礎路由的網站</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 使用者</p></td>
<td><p>允許同時響鈴</p></td>
<td><p>不允許同時響鈴</p></td>
<td><p>不允許同時響鈴</p></td>
</tr>
</tbody>
</table>

  
下表說明來自位於相同網站、不同網站或未知網站之 Lync 使用者 (亦即 Lync 來電者) 的通話。受話者的 PSTN 端點 (亦即行動電話) 設為同步響鈴目標。在此案例中，位置基礎路由會判斷是否應將通話路由傳送到受話者的同步響鈴目標 (亦即行動電話)。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>同步響鈴目標</th>
<th>位於與受話者相同的網站</th>
<th>位於與受話者不同的網站</th>
<th>位於未知網站或未啟用位置基礎路由的網站</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PSTN 端點</p></td>
<td><p>允許透過來電者的網站語音路由原則同步響鈴</p></td>
<td><p>允許透過來電者的網站語音路由原則同步響鈴</p></td>
<td><p>允許透過來電者的語音原則對未啟用位置基礎路由的主幹同步響鈴</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 其他資源

[Lync Server 2013 中的位置基礎路由案例](lync-server-2013-scenarios-for-location-based-routing.md)

