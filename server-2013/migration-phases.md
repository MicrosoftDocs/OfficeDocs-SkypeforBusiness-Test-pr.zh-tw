---
title: 移轉階段
TOCTitle: 移轉階段
ms:assetid: cb7747ba-b872-42ca-ab41-76e3c4e77d06
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205336(v=OCS.15)
ms:contentKeyID: 49292328
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉階段

 

_**上次修改主題的時間：** 2012-09-17_

在 Lync Server 2013 中，您可定義您網站上包含 Lync Server 2013 元件的「網站」。網站是一群透過高速且低延遲的網路互連的電腦，例如單一區域網路 (LAN) 或以高速光纖網路連接的兩個網路。

「前端集區」 是一組以相同方式設定的前端伺服器，其共同運作以提供服務給一般使用者群組。集區可為您的使用者提供延展性及容錯移轉功能。集區中的每部伺服器都必須執行一或多個相同的伺服器角色。專為小型組織設計的 Standard Edition 伺服器也會定義集區，並且在單一伺服器上執行。這可讓您以較少的成本擁有 Lync Server 2013 功能，但所提供的解決方案未真正具有高可用性。

下列階段說明從 Lync Server 2010 集區移轉至 Lync Server 2013 的處理程序。若是包含多個集區的多重網站，每個各別的集區都應遵循此階段式方法進行。

1.  [第 1 階段：規劃從 Lync Server 2010 進行移轉](phase-1-plan-your-migration-from-lync-server-2010.md)

2.  [第 2 階段：準備移轉](phase-2-prepare-for-migration.md)

3.  [第 3 階段：部署 Lync Server 2013 試驗集區](phase-3-deploy-lync-server-2013-pilot-pool.md)

4.  [第 4 階段：將測試使用者移至試驗集區](phase-4-move-test-users-to-the-pilot-pool.md)

5.  [第 5 階段：將 Lync Server 2013 Edge Server 新增至試驗集區](phase-5-add-lync-server-2013-edge-server-to-pilot-pool.md)

6.  [第 6 階段：從試驗部署移至生產](phase-6-move-from-pilot-deployment-into-production.md)

7.  [第 7 階段：完成移轉後工作](phase-7-complete-post-migration-tasks.md)

8.  [第 8 階段：解除委任舊版集區](phase-8-decommission-legacy-pools.md)

