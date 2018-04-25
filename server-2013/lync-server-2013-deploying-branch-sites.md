---
title: Lync Server 2013：部署分支網站
TOCTitle: 部署分支網站
ms:assetid: 1475dee0-66ae-4ee5-b6f1-7409b4bbff45
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398217(v=OCS.15)
ms:contentKeyID: 49290180
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中部署分支網站

 

_**上次修改主題的時間：** 2012-09-21_

分支網站使用者會從分支網站關聯的中央網站伺服器，取得大部分 Lync Server 2013 功能。每個分支網站都恰與一個中央網站關聯。若要與公用交換電話網路 (PSTN) 傳送通話，分支網站可能包含下列任一項：

  - PSTN 閘道，以及可能包含中繼伺服器

  - SIP 主幹

  - 現有語音基礎結構搭配專用交換機 (PBX)

  - 一部 Survivable Branch Appliance

  - 一部 Survivable Branch 伺服器

具備 Survivable Branch Appliance 或 Survivable Branch 伺服器的分支網站在廣域網路或中央網站故障期間，會比不具任一解決方案的分支網站更有恢復能力。例如，在已部署 Survivable Branch Appliance 或 Survivable Branch 伺服器的網站中，如果從分支網站連接至中央網站的網路故障，使用者仍然可以撥打和接聽 PSTN 電話。另外一個提供分支網站恢復的方法是，使用 PSTN 閘道或 SIP 主幹 (其在分支網站有完整的 Lync Server 部署)。

如需哪種分支網站部署最適合組織的詳細資訊，包括先決條件和其他規劃考量事項，請參閱規劃文件中的＜ [在 Lync Server 2013 中規劃 PSTN 連線](lync-server-2013-planning-for-pstn-connectivity.md)＞及＜ [在 Lync Server 2013 中規劃分支網站語音彈性](lync-server-2013-planning-for-branch-site-voice-resiliency.md)＞。

## 本章節內容

  - [使用 Lync Server 2013 在分支網站提供 PSTN 連線](lync-server-2013-providing-pstn-connectivity-at-a-branch-site.md)

  - [使用 Lync Server 2013 部署 Survivable Branch Appliance 或 Survivable Branch Server](lync-server-2013-deploying-a-survivable-branch-appliance-or-server.md)

