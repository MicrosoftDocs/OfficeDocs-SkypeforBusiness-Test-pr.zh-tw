---
title: Lync Server 2013：部署概觀
TOCTitle: 部署概觀
ms:assetid: da67555e-f410-4c37-9996-d511f37da8d1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205305(v=OCS.15)
ms:contentKeyID: 49292507
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的部署概觀

 

_**上次修改主題的時間：** 2013-03-12_

Lync Server 2013  Enterprise Edition 與 Lync Server 2013  Standard Edition 之間的主要差異在於， Standard Edition 不支援 Enterprise Edition 隨附的高可用性功能。您必須對一個集區部署多個 前端伺服器，然後鏡像執行 SQL Server 的伺服器，才能提供高可用性。使用 Enterprise Edition 時，您可以選擇組合或定義獨立 中繼伺服器。 監控伺服器與 封存伺服器可以使用執行 SQL Server 的獨立伺服器。或者，可以在 前端伺服器與集區所用的資料庫伺服器上，執行 SQL Server 執行個體。

執行 Lync Server 2013Standard Edition 的伺服器主要適用於較小型的組織以及地理位置不在組織的主要部署範圍內的遠端位置。兩部可供災難發生時進行容錯移轉的 Standard Edition 伺服器 伺服器配對在一起，可以支援多達 5,000 位使用者。和在 Enterprise Edition 中的 前端伺服器 不同，您無法聚集 Standard Edition 伺服器。此外， Standard Edition 使用的 SQL Server 資料庫是執行 SQL Server Express 的組合伺服器，專為處理 Standard Edition 伺服器 工作量而設計。這並不代表所有角色都必須位於 Standard Edition 伺服器。您可以有獨立的 中繼伺服器 與 Edge Server。可供 中央管理存放區使用及專供 Lync Server 2013 之用的 SQL Server 資料庫，必須位於 Standard Edition 伺服器，其與執行 SQL Server 的伺服器組合在一起。 監控伺服器與 封存伺服器都會使用包含 SQL Server 資料庫的獨立伺服器。

