---
title: 在 Lync Server 2013 中設定企業語音
TOCTitle: 在 Lync Server 2013 中設定企業語音
ms:assetid: 7df179fa-d3a2-4b23-a433-b750aedf980b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994041(v=OCS.15)
ms:contentKeyID: 52056133
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定企業語音

 

_**上次修改主題的時間：** 2015-03-09_

若要部署企業語音，需要設定下列項目：

  - 建立主幹

  - 定義語音原則

  - 定義語音路由

  - 允許使用者使用企業語音

## 建立主幹

您必須在 企業語音 部署中定義主幹。對於位置基礎路由，您必須為每個主幹建立主幹組態。使用 Lync Server拓撲產生器 定義您的主幹，並使用 Lync ServerWindows PowerShell 命令 New-CsTrunkConfiguration 或 Lync Server 控制台 定義對應的主幹組態。更多有關如何在主幹組態上啟用位置基礎路由的資訊，可以在主題[在 Lync Server 2013 中啟用位置基礎路由](lync-server-2013-enabling-location-based-routing.md) 中的＜對主幹啟用位置基礎路由＞一節找到。就此範例而言，下表說明此案例中使用的主幹。

如需詳細資訊，請參閱＜[在 Lync Server 2013 中使用拓撲產生器定義其他主幹](lync-server-2013-define-additional-trunks-in-topology-builder.md)＞。


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
<th>主幹名稱</th>
<th>系統類型</th>
<th>名稱</th>
<th>位置</th>
<th>中繼伺服器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主幹 1 DEL-GW</p></td>
<td><p>PSTN 閘道</p></td>
<td><p>DEL-GW</p></td>
<td><p>Delhi</p></td>
<td><p>MS1</p></td>
</tr>
<tr class="even">
<td><p>主幹 2 HYD-GW</p></td>
<td><p>PSTN 閘道</p></td>
<td><p>HYD-GW</p></td>
<td><p>Hyderabad</p></td>
<td><p>MS1</p></td>
</tr>
<tr class="odd">
<td><p>主幹 3 DEL-PBX</p></td>
<td><p>PBX</p></td>
<td><p>DEL-PBX</p></td>
<td><p>Delhi</p></td>
<td><p>MS1</p></td>
</tr>
<tr class="even">
<td><p>主幹 4 HYD-PBX</p></td>
<td><p>PBX</p></td>
<td><p>HYD-PBX</p></td>
<td><p>Hyderabad</p></td>
<td><p>MS1</p></td>
</tr>
</tbody>
</table>



## 定義語音原則

您必須為您的 企業語音 部署定義語音原則。如果只有一部分使用者需要使用位置基礎路由，請定義語音原則，對部分使用者執行位置基礎路由限制。就此範例而言，下表說明此案例中使用的語音原則。表中只包括位置基礎路由的特有設定，做為說明之用。

如需詳細資訊，請參閱＜[在 Lync Server 2013 中設定用於授權撥號功能和權限的語音原則和 PSTN 使用方式記錄](lync-server-2013-configuring-voice-policies-and-pstn-usage-records-to-authorize-calling-features-and-privileges.md)＞。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>語音原則 1</th>
<th>語音原則 2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>語音原則識別碼</p></td>
<td><p>Delhi 語音原則</p></td>
<td><p>Hyderabad 語音原則</p></td>
</tr>
<tr class="even">
<td><p>PSTN 使用方式</p></td>
<td><p>Delhi 使用方式、PBX Del 使用方式、PBX Hyd 使用方式</p></td>
<td><p>Hyderabad 使用方式、PBX Hyd 使用方式、PBX Del 使用方式</p></td>
</tr>
<tr class="odd">
<td><p>PreventPSTNTollBypass</p></td>
<td><p>False</p></td>
<td><p>False</p></td>
</tr>
</tbody>
</table>



## 定義語音路由

您必須為您的 企業語音 部署定義語音路由。就此範例而言，下表說明此案例中使用的語音路由。表中只包括位置基礎路由的特有設定，做為說明之用。

如需詳細資訊，請參閱＜[Lync Server 2013 中設定撥出電話的語音路由](lync-server-2013-configuring-voice-routes-for-outbound-calls.md)＞。


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
<th></th>
<th>語音路由 1</th>
<th>語音路由 2</th>
<th>語音路由 3</th>
<th>語音路由 4</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>名稱</p></td>
<td><p>Delhi 路由</p></td>
<td><p>Hyderabad 路由</p></td>
<td><p>PBX Del 路由</p></td>
<td><p>PBX Hyd 路由</p></td>
</tr>
<tr class="even">
<td><p>PSTN 使用方式</p></td>
<td><p>Delhi 使用方式</p></td>
<td><p>Hyderabad 使用方式</p></td>
<td><p>PBX Del 使用方式</p></td>
<td><p>PBX Hyd 使用方式</p></td>
</tr>
<tr class="odd">
<td><p>主幹</p></td>
<td><p>主幹 1 DEL-GW</p></td>
<td><p>主幹 2 HYD-GW</p></td>
<td><p>主幹 3 DEL-PBX</p></td>
<td><p>主幹 4 HYD-PBX</p></td>
</tr>
</tbody>
</table>



## 允許使用者使用企業語音

允許使用者使用企業語音並指派您先前定義的語音原則。就此範例而言，下表說明此案例中使用的指派。表中只包括位置基礎路由的特有設定，做為說明之用。

如需詳細資訊，請參閱＜[在 Lync Server 2013 中為使用者啟用企業語音](lync-server-2013-enable-users-for-enterprise-voice.md)＞。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>位於 Delhi 的使用者</th>
<th>位於 Hyderabad 的使用者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>關聯的語音原則</p></td>
<td><p>Delhi 語音原則</p></td>
<td><p>Hyderabad 語音原則</p></td>
</tr>
<tr class="even">
<td><p>範例使用者</p></td>
<td><p>DEL-LYNC-1、DEL-LYNC-2、DEL-LYNC-3</p></td>
<td><p>HYD-LYNC-1、HYD-LYNC-2、HYD-LYNC-3</p></td>
</tr>
</tbody>
</table>



## 請參閱

#### 其他資源

[在 Lync Server 2013 中設定位置基礎路由](lync-server-2013-configuring-location-based-routing.md)

