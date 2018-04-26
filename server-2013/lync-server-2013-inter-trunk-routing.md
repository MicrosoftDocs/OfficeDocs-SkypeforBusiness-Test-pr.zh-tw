---
title: Lync Server 2013：主幹間路由
TOCTitle: 主幹間路由
ms:assetid: f687a548-1f2e-48ed-9745-a13dc1f3698f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721940(v=OCS.15)
ms:contentKeyID: 49890511
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的主幹間路由

 

_**上次修改主題的時間：** 2012-10-08_

Lync Server 2013 透過支援主部間路由來提供基本工作階段管理。這項新功能可讓 Lync Server 提供下游拓撲系統通話控制功能。主幹間路由可將 IP-PBX 與公用交換電話網路 (PSTN) 閘道相互連接，因此可將專用交換機 (PBX) 的通話路由傳遞至 PSTN，將傳入的 PSTN 通話路由傳遞至 PBX 電話。同理， Lync Server 可相互連接兩組以上的 IP-PBX 系統，因此 PBX 電話間可播出與接收來自不同 IP-PBX 系統的通話。

下圖說明 Lync Server 2013 提供 PSTN 閘道與 IP-PBX 間的相互連接。

![連接 PSTN 閘道/IP-PBX 圖表的 Lync Server](images/JJ721940.cc3858ca-2ee3-4d51-8a51-db078366b50b(OCS.15).jpg "連接 PSTN 閘道/IP-PBX 圖表的 Lync Server")

下圖說明連接兩個 IP-PBX 系統的 Lync Server 2013。

![交互連接 IP-PAX 系統圖表的 Lync Server](images/JJ721940.6ba18ec9-df70-498a-9cf7-7fc41e5ec432(OCS.15).jpg "交互連接 IP-PAX 系統圖表的 Lync Server")

