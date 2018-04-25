---
title: Lync Server 2013：保護傳輸的資料 - 封存、監控、群組交談規範伺服器資料庫
TOCTitle: 在 Lync Server 2013 中保護傳輸的資料 - 封存、監控、群組交談規範伺服器資料庫
ms:assetid: ea219705-1015-43a7-890b-e7e67b451e7c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn518336(v=OCS.15)
ms:contentKeyID: 60471202
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中保護傳輸的資料 - 封存、監控、群組交談規範伺服器資料庫

 

_**上次修改主題的時間：** 2013-12-05_

Microsoft Lync Server 2013 封存伺服器和監控伺服器都是使用訊息佇列 (也稱為 MSMQ) 服務來收集資料訊息，並將這些訊息可靠地從收集點移至儲存機制伺服器。規範服務也是使用訊息佇列，以協同群組聊天伺服器收集資料。

在 Lync Server 2013 中，沒有為傳輸中的資料提供內部保護。不過，如果必須保護這類流量，訊息佇列服務能夠在傳送端訊息佇列上提供訊息層級的加密。這個功能是使用 Active Directory 網域服務管理的憑證來達成。如需詳細資料，請參閱＜附錄 D：Windows Server 2008 中的訊息佇列與網際網路通訊＞，網址為 [http://go.microsoft.com/fwlink/p/?LinkId=145238](http://go.microsoft.com/fwlink/p/?linkid=145238)，或若是使用 Windows Server 2008 R2，請參閱＜附錄 I：Windows Server 2008 R2 中的訊息佇列和網際網路通訊＞(英文)，網址為 [http://go.microsoft.com/fwlink/p/?LinkId=211883](http://go.microsoft.com/fwlink/p/?linkid=211883)。

