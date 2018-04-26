---
title: 移除後端伺服器上的 SQL Server 執行個體與資料庫
TOCTitle: 移除後端伺服器上的 SQL Server 執行個體與資料庫
ms:assetid: 32457df9-7dd9-4fca-9362-ea4de26b0296
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688016(v=OCS.15)
ms:contentKeyID: 49890011
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移除後端伺服器上的 SQL Server 執行個體與資料庫

 

_**上次修改主題的時間：** 2012-10-19_

若要移除 Microsoft SQL Server 資料庫與執行個體，您可先移除與其相依且執行 Lync Server 2010 的伺服器，或者，您可先重新設定執行 Lync Server 2010 的伺服器以使用其他資料庫，再將該資料庫與執行個體移除。在撤銷目前的 SQL Server 或重新設定執行 Lync Server 2010 的目前伺服器使其將資料庫轉譯為過時或無法使用時，您必須執行本主題中的這項程序。

若要移除 封存伺服器或 監控伺服器的資料庫或執行個體，您必須先移除伺服器角色。同樣地，若要移除 前端集區的執行個體或資料庫，您必須先移除或重新設定相依伺服器角色。不論是針對伺服器的組合資料庫或個別執行個體，這些程序都是一樣的。組合資料庫並不會影響這些程序。

## 本章節內容

  - [移除前端集區的 SQL Server 資料庫](remove-the-sql-server-database-for-a-front-end-pool.md)

  - [移除監控伺服器的 SQL Server 資料庫](remove-the-sql-server-database-for-a-monitoring-server.md)

  - [移除封存伺服器的 SQL Server 資料庫](remove-the-sql-server-database-for-an-archiving-server.md)

