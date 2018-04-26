---
title: Lync Server 2013：為 Lync Server 2013 設定 SQL Server
TOCTitle: 為 Lync Server 2013 設定 SQL Server
ms:assetid: 375e5cc4-e436-46dc-9b02-5063f35cdcc1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425848(v=OCS.15)
ms:contentKeyID: 49290584
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 為 Lync Server 2013 設定 SQL Server

 

_**上次修改主題的時間：** 2013-08-12_

此區段中的主題討論如何部署及設定 SQL Server，以用於 Lync Server 的企業部署。 Standard Edition 伺服器使用 SQL Server 的組合 SQL Server Express 版本，這對於 Standard Edition 伺服器的工作負載是大小恰當的。

Lync Server 2013  中央管理存放區會保留集區中所有 Enterprise Edition 的使用者資料，且依設計應位於 SQL Server 後端伺服器上。作為中央存放庫的後端資料庫， 中央管理存放區不能同任何其他 Lync Server 2013 角色一般安裝在同一部電腦上。 中央管理存放區不能位於集區中的 Enterprise Edition 上。當您首次發行拓撲並選取建立資料庫時，就會自動建立 中央管理存放區。您指定作為後端伺服器的電腦必須已執行 SQL Server 資料庫軟體，安裝才會成功。

## 本章節內容

  - [Lync Server 2013 的 SQL Server 資料和記錄檔位置](lync-server-2013-sql-server-data-and-log-file-placement.md)

  - [在 Lync Server 2013 中設定 SQL Server](lync-server-2013-configure-sql-server.md)

  - [Lync Server 2013 中 SQL Server 的部署權限](lync-server-2013-deployment-permissions-for-sql-server.md)

  - [在 Lync Server 2013 中使用 Lync Server 管理命令介面安裝資料庫](lync-server-2013-database-installation-using-lync-server-management-shell.md)

  - [瞭解與 Lync Server 2013 搭配使用時之 SQL Server 的防火牆需求](lync-server-2013-understanding-firewall-requirements-for-sql-server.md)

  - [在 Lync Server 2013 中設定 SQL Server 叢集](lync-server-2013-configure-sql-server-clustering.md)

