---
title: Lync Server 2013：設定位置基礎路由
TOCTitle: 設定位置基礎路由
ms:assetid: 63cdc474-e80f-43b1-a237-9d9ed673300a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994036(v=OCS.15)
ms:contentKeyID: 52056118
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定位置基礎路由

 

_**上次修改主題的時間：** 2015-03-09_

Lync Server 2013 CU1 位置基礎路由是一項 企業語音功能。位置基礎路由是通話管理功能，可以控制 Lync Server 2013 CU1 路由傳送通話的方式。它可以根據 Lync 來電者的位置，對於應將通話路由傳送到 PBX 或 PSTN 目的地強制加以限制。位置基礎路由會根據來電者的網路位置，將通話授權規則套用到 PSTN 通話。來電者的位置是根據與來電者連線之子網路相關聯的網站加以判斷。要設定位置基礎路由，需要先部署 企業語音，接著設定網路區域、網站和子網路。如此即可建立啟用位置基礎路由的基礎。

在部署位置基礎路由之前，必須先部署企業語音，以及設定網路區域、網站，並將子網路與網站建立關聯。完成後，您就可以設定位置基礎路由。如需有關如何設定網路區域、網站和子網路的步驟，請參閱＜ [在 Lync Server 2013 中部署進階 Enterprise Voice 功能](lync-server-2013-deploying-advanced-enterprise-voice-features.md)＞。

本節會使用下列範例進行說明，引導您完成設定位置基礎路由的作業。

![Enterprise Voice 以位置為基礎的路由範例](images/JJ994036.b6ef5afc-36ac-406f-8ec2-a87532b20612(OCS.15).png "Enterprise Voice 以位置為基礎的路由範例")

  
下表中的內容表示此範例中定義的使用者。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>端點類型</th>
<th>位置</th>
<th>使用者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync</p></td>
<td><p>德里企業辦公室</p></td>
<td><p>DEL-LYNC-1、DEL-LYNC-2、DEL-LYNC-3</p></td>
</tr>
<tr class="even">
<td><p>Lync</p></td>
<td><p>海德拉巴企業辦公室</p></td>
<td><p>HYD-LYNC-1、HYD-LYNC-2、HYD-LYNC-3</p></td>
</tr>
<tr class="odd">
<td><p>Lync</p></td>
<td><p>未知 (例如飯店)</p></td>
<td><p>UNK-LYNC-1</p></td>
</tr>
<tr class="even">
<td><p>PBX</p></td>
<td><p>德里企業辦公室</p></td>
<td><p>DEL-PBX-1、DEL-PBX-2</p></td>
</tr>
<tr class="odd">
<td><p>PBX</p></td>
<td><p>海德拉巴企業辦公室</p></td>
<td><p>HYD-PBX-1、HYD-PBX-2</p></td>
</tr>
<tr class="even">
<td><p>PSTN</p></td>
<td><p>未知</p></td>
<td><p>PSTN-1、PSTN-2、PSTN-3</p></td>
</tr>
</tbody>
</table>

  

下表中的內容表示此範例環境中說明的使用者。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>系統</th>
<th>位置</th>
<th>名稱</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync Server 2013 CU1 集區</p></td>
<td><p>任何</p></td>
<td><p>LS-PL1</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2013 CU1、 中繼伺服器</p></td>
<td><p>任何</p></td>
<td><p>MS-PL1</p></td>
</tr>
<tr class="odd">
<td><p>PSTN 閘道 1</p></td>
<td><p>德里</p></td>
<td><p>DEL-GW</p></td>
</tr>
<tr class="even">
<td><p>PSTN 閘道 2</p></td>
<td><p>海德拉巴</p></td>
<td><p>HYD-GW</p></td>
</tr>
<tr class="odd">
<td><p>PBX 1</p></td>
<td><p>德里</p></td>
<td><p>DEL-PBX</p></td>
</tr>
<tr class="even">
<td><p>PBX 2</p></td>
<td><p>海德拉巴</p></td>
<td><p>RED-PBX</p></td>
</tr>
</tbody>
</table>


## 本章節內容

  - [在 Lync Server 2013 中設定企業語音](lync-server-2013-configuring-enterprise-voice.md)

  - [在 Lync Server 2013 中部署網路區域、網站和子網路](lync-server-2013-deploying-network-regions-sites-and-subnets.md)

  - [在 Lync Server 2013 中啟用位置基礎路由](lync-server-2013-enabling-location-based-routing.md)

## 請參閱

#### 其他資源

[在 Lync Server 2013 中部署進階 Enterprise Voice 功能](lync-server-2013-deploying-advanced-enterprise-voice-features.md)

