---
title: 備份及還原 Lync Server 2013
TOCTitle: 備份及還原 Lync Server 2013
ms:assetid: 07dc1f5e-af66-4e18-bf39-881dceff8bc3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202160(v=OCS.15)
ms:contentKeyID: 52056046
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 備份及還原 Lync Server 2013

 

_**上次修改主題的時間：** 2013-02-21_

您將在本節中找到備份 Lync Server 2013 資料，以及失敗時還原資料的最佳作法。這些最佳作法可適用於下列情況︰

  - 任何類型的整個 Lync Server 集區 (前端伺服器、Edge Server、中繼伺服器、常設聊天室伺服器 或 Director) 或這些集區中的個別伺服器。

  - 中央管理伺服器­ 

  - Standard Edition Server

  - Enterprise Edition 後端伺服器

  - 檔案存放區 

  - 封存資料庫、監控資料庫或常設聊天室資料庫

本節不包含還原整個網台或開發待命網站的相關資訊。如需以配對前端集區來開發災害復原解決方案的詳細資訊，請參閱＜[在 Lync Server 2013 中規劃高可用性和災害復原](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)＞。這是災害復原規劃的建議方法。

若已部署配對前端集區，則當其中一個集區失敗且無法復原時，就可利用其配對集區之新的完整網域名稱 (FQDN)，還原此集區。如需執行此復原步驟的詳細資訊，請參閱＜[在 Lync Server 2013 中容錯移轉集區](lync-server-2013-failing-over-a-pool.md)＞。此外，若之後想要重新建立前端配對中失敗且無法復原的集區，則可使用＜[執行 ABC 前端集區容錯移轉](lync-server-2013-performing-an-abc-front-end-pool-failover.md)＞中的步驟。

本文件中所說明的方法在規劃階段涉及特殊考量。如需詳細資訊，請參閱＜[建立備份和還原規劃](lync-server-2013-establishing-a-backup-and-restoration-plan.md)＞。

## 本章節內容

  - [準備 Lync Server 備份和還原](lync-server-2013-preparing-for-lync-server-backup-and-restoration.md)

  - [備份資料和設定](lync-server-2013-backing-up-data-and-settings.md)

  - [還原資料和設定](lync-server-2013-restoring-data-and-settings.md)

  - [備份和還原工作表](lync-server-2013-backup-and-restoration-worksheets.md)

