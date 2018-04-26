---
title: Lync Server 2013：將延伸的常設聊天室伺服器集區用於災害復原
TOCTitle: 將延伸的常設聊天室伺服器集區用於災害復原
ms:assetid: 74c5287e-d70d-490a-9adc-ab419917ddd9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205007(v=OCS.15)
ms:contentKeyID: 49291321
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中將延伸的常設聊天室伺服器集區用於災害復原

 

_**上次修改主題的時間：** 2012-10-06_

適用於 常設聊天室伺服器 的災害復原解決方案建立在延伸的 Persistent Chat Server 集區上。這種作法類似於 Lync Server 2010 中的本地網站恢復能力；但是，並不需要延伸的虛擬區域網路 (VLAN)。透過延伸 Persistent Chat Server 集區，基本上您要以邏輯方式在拓撲中設定一個集區，但需要實際將伺服器置於兩個不同資料中心的集區。請以相同方式設定資料庫的 SQL Server 鏡像，並在同一個資料中心部署資料庫及鏡像。您必須在次要資料中心設定備份資料庫 (包含於災害復原期間提供高可用性的選用鏡像)。此為在災害復原期間用於容錯移轉的備份資料庫。

如需有關如何設定高可用性 SQL Server 鏡像的詳細資訊，請參閱 [Lync Server 2013 中的 SQL Server 鏡像](lync-server-2013-sql-server-mirroring.md)。如需有關容錯移轉適用於災害復原之資料庫的詳細資訊，請參閱＜ [在 Lync Server 2013 中針對常設聊天室伺服器主要資料庫設定 SQL Server 記錄傳送](lync-server-2013-setting-up-sql-server-log-shipping-for-the-persistent-chat-server-primary-database.md)＞及＜ [在 Lync Server 2013 中設定主要鏡像與記錄傳送次要資料庫之間的 SQL Server 記錄傳送](lync-server-2013-setting-up-sql-server-log-shipping-between-the-primary-mirror-and-the-log-shipping-secondary-database.md)＞。

