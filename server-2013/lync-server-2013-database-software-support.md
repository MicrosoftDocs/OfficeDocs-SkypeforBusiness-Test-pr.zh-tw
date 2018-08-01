---
title: Lync Server 2013 資料庫軟體支援
TOCTitle: 資料庫軟體支援
ms:assetid: e05d0032-bbea-4e61-987d-d07b1c045fd5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398990(v=OCS.15)
ms:contentKeyID: 49292577
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的資料庫軟體支援

 

_**上次修改主題的時間：** 2014-12-01_

Lync Server 2013 支援下列資料庫管理系統：

  - **前端集區的後端資料庫、封存資料庫、監控資料庫、常設聊天室資料庫以及常設聊天室規範資料庫**
    
      - Microsoft SQL Server 2008 R2 Enterprise 資料庫軟體 (64 位元版本)。建議額外執行最新的 Service Pack。
    
      - Microsoft SQL Server 2008 R2 Standard (64 位元版本)。建議額外執行最新的 Service Pack。
    
      - Microsoft SQL Server 2012 Enterprise (64 位元版本)。建議額外執行最新的 Service Pack。
    
      - Microsoft SQL Server 2012 Standard (64 位元版本)。建議額外執行最新的 Service Pack。

  - **Standard Edition Server 資料庫與前端伺服器資料庫**
    
      - Microsoft SQL Server 2012 Express (64 位元版本)。另外建議執行最新的 Service Pack。
        
        我們支援在前端伺服器和 Standard Edition 伺服器 上進行 Microsoft SQL Server 的修補與升級作業。不過，在前端伺服器上進行任何形式的升級及修補時，都必須將仲裁需求列入考量。如需詳細資訊，請參閱[在 Lync Server 2013 中升級或更新前端伺服器](lync-server-2013-upgrade-or-update-front-end-servers.md)及 [Lync Server 2013 中的前端伺服器、立即訊息及顯示狀態的拓撲和元件](lync-server-2013-topologies-and-components-for-front-end-servers-instant-messaging-and-presence.md)。
    
    > [!NOTE]  
    > Lync Server 2013 會自動將 Microsoft SQL Server 2012 Express (64 位元版本) 安裝在各個 Standard Edition Server 和各個前端伺服器。
    


> [!IMPORTANT]  
> <ul>
> <li><p>Lync Server 2013 不支援 SQL Server 32 位元版本。您必須使用 64 位元版本。</p></li>
> <li><p>不支援 SQL Server Web Edition 和 SQL Server Workgroup Edition。您無法使用者兩種版本搭配 Lync Server 2013。</p></li>
> <li><p>Lync Server 2013 確實支援原生資料庫鏡像功能。</p></li>
> <li><p>若要使用監控伺服器角色，您應該安裝 SQL Server Reporting Services。</p></li>
> </ul>

在前端集區中，後端資料庫可以是單一 SQL Server 電腦。

> [!IMPORTANT]  
> 如果您將 Lync Server 資料庫與其他資料庫組合在一起，強烈建議評估可能影響可用性和效能的所有因素，並確定某個節點失敗時，其餘節點可以處理負載。若要確認容錯移轉功能，建議測試所有容錯移轉案例。



## 使用 SQL 鏡像與 SQL 叢集

Lync Server 2013 支援各個 Lync Server 資料庫中對於 SQL 鏡像或 SQL 叢集的使用。您可以在 Lync Server 2013 中使用 拓撲產生器工具輕鬆設定 SQL 鏡像。對於 SQL 容錯移轉叢集，您必須使用 SQL Server 進行設定。

Lync Server 2013 支援各式部署的 SQL 鏡像與 SQL 叢集拓撲，包括已從先前版本的 Lync Server 升級的嶄新部署與組織。

SQL 叢集支援適用於主動/被動組態。基於效能因素，被動節點不應由任何其他 SQL 執行個體共用。

以下支援包含在內：

  - 適用於下列項目的雙節點容錯移轉叢集：
    
      - Microsoft SQL Server 2012 Standard (64 位元版本)。建議額外執行最新的 Service Pack。
    
      - Microsoft SQL Server 2008 R2 Standard (64 位元版本)。建議額外執行最新的 Service Pack。

  - 適用於下列項目、最多可有 16 個節點的容錯移轉叢集：
    
      - Microsoft SQL Server 2012 Enterprise (64 位元版本)。建議額外執行最新的 Service Pack。
    
      - Microsoft SQL Server 2008 R2 Enterprise 資料庫軟體 (64 位元版本)。建議額外執行最新的 Service Pack。

如需 SQL 鏡像的詳細資訊，請參閱＜ [Lync Server 2013 中的後端伺服器高可用性](lync-server-2013-back-end-server-high-availability.md)＞。如需如何部署 SQL 叢集的詳細資料，請參閱＜ [在 Lync Server 2013 中設定 SQL Server 叢集](lync-server-2013-configure-sql-server-clustering.md)＞。

如需在 SQL Server 2012 中進行容錯移轉叢集的詳細資訊與最佳做法，請參閱 <http://technet.microsoft.com/zh-tw/library/hh231721.aspx>。如需在 SQL Server 2008 中進行容錯移轉叢集的詳細資訊，請參閱 <http://technet.microsoft.com/zh-tw/library/ms189134(v=sql.105).aspx>。

