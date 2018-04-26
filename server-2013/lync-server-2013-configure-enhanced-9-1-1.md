---
title: Lync Server 2013：設定增強型 9-1-1
TOCTitle: 設定增強型 9-1-1
ms:assetid: 5967de00-c8b9-4923-86da-6ad3369a4cad
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398390(v=OCS.15)
ms:contentKeyID: 49291003
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定增強型 9-1-1

 

_**上次修改主題的時間：** 2013-02-24_

增強型 9-1-1 (E9-1-1) 是緊急通知功能，會讓來電者的電話號碼與市街地址產生關聯。使用這項資訊，公共安全勤務中心 (PSAP) 可以立即派遣緊急服務人員到需要幫助的來電者所在處。

若要支援 E9-1-1，Lync Server 2013 必須能正確關聯位置與用戶端，並確定使用此資訊，將緊急通話路由傳送至最近的 PSAP。

如需有關規劃 E9-1-1 部署的詳細資訊，請參閱＜ [在 Lync Server 2013 中規劃緊急服務 (E9-1-1)](lync-server-2013-planning-for-emergency-services-e9-1-1.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 2013 僅支援美國境內的 E9-1-1。若要部署 E9-1-1，您必須設定與合格的 E9-1-1 服務提供者的 SIP 連線，或者將緊急位置識別號碼 (ELIN) 閘道部署至以公用交換電話網路 (PSTN) 為基礎的 E9-1-1 服務提供者。如需詳細資訊，請參閱＜ <a href="lync-server-2013-enhanced-9-1-1-e9-1-1-and-mediation-server.md">Lync Server 2013 中的增強型 9-1-1 (E9-1-1) 和中繼伺服器</a>＞。如需設定主幹連線的詳細資訊，請參閱＜ <a href="lync-server-2013-configure-a-trunk-with-media-bypass.md">在 Lync Server 2013 中設定含媒體旁路的主幹</a>＞。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [在 Lync Server 2013 中設定 E9-1-1 語音路由](lync-server-2013-configure-an-e9-1-1-voice-route.md)

  - [在 Lync Server 2013 中建立位置原則](lync-server-2013-create-location-policies.md)

  - [在 Lync Server 2013 中為 E9-1-1 設定網站資訊](lync-server-2013-configure-site-information-for-e9-1-1.md)

  - [在 Lync Server 2013 中設定位置資料庫](lync-server-2013-configure-the-location-database.md)

  - [在 Lync Server 2013 中設定進階 E9-1-1 功能](lync-server-2013-configure-advanced-e9-1-1-features.md)

