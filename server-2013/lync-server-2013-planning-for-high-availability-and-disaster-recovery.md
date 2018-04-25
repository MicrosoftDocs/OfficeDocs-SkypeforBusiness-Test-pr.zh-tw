---
title: Lync Server 2013：規劃高可用性和災害復原
TOCTitle: 規劃高可用性和災害復原
ms:assetid: 15a72073-0336-45dd-b2a0-35e7522c6000
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204703(v=OCS.15)
ms:contentKeyID: 49290194
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中規劃高可用性和災害復原

 

_**上次修改主題的時間：** 2013-10-31_

就像在 Lync Server 2010 中， Lync Server 2013 中大部分伺服器角色的主要高可用性配置是根據透過集區的伺服器備援。如果執行特定伺服器角色的伺服器失敗，集區中執行相同角色的其他伺服器就會接手該伺服器的負載。這適用於前端伺服器、Edge Server、中繼伺服器及 Director。

Lync Server 2013 新增前端集區的災害復原措施，其將伺服器的地理分佈導入兩個資料中心，萬一有一整個集區或網站當機時，可以讓服務繼續。

Lync Server 2013 也增強了後端伺服器高可用性，可支援後端資料庫的同步 SQL 鏡像。

本節說明這些主要高可用性和災害復原功能，另外也會說明您可以針對其他伺服器角色的高可用性和災害復原採取哪些步驟。

## 本節內容

  - [Lync Server 2013 中的前端集區災害復原](lync-server-2013-front-end-pool-disaster-recovery.md)

  - [Lync Server 2013 中的 Edge Server 災害復原](lync-server-2013-edge-server-disaster-recovery.md)

  - [在 Lync Server 2013 中規劃企業語音復原](lync-server-2013-planning-for-enterprise-voice-resiliency.md)

  - [Lync Server 2013 中的災害復原通話管理功能](lync-server-2013-call-management-features-for-disaster-recovery.md)

  - [在 Lync Server 2013 中針對高可用性和災害復原設定常設聊天室伺服器](lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md)

  - [Lync Server 2010 都會區網站復原](lync-server-2013-compatibility-with-lync-server-2010-metropolitan-site-resiliency.md)

