---
title: 將監視報告與鏡像資料庫相關聯
TOCTitle: 將監視報告與鏡像資料庫相關聯
ms:assetid: 42b797c6-8db8-4ad7-886e-8ddf8deb06f9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945624(v=OCS.15)
ms:contentKeyID: 52056095
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將監視報告與鏡像資料庫相關聯

 

_**上次修改主題的時間：** 2014-02-07_

如果您設定鏡像來監控資料庫，如果發生容錯移轉，該鏡像資料庫將會接手成為主要資料庫。但是，如果您使用 Lync Server「監視報告」並發生容錯移轉，您可能會發現您的「監視報告」不會連線至鏡像資料庫。這是因為，當您安裝「監視報告」時，您只指定了主要資料庫的位置；您不會指定鏡像資料庫的位置。

若要使「監視報告」自動容錯移轉至鏡像資料庫，您必須將鏡像資料庫做為「容錯移轉合作夥伴」新增至「監視報告」所使用的兩個資料庫 (一個資料庫用於「通話詳細資訊記錄」資料，另一個資料庫用於「經驗品質」(QoE) 資料)。(請注意，此步驟應於您安裝「監視報告」之後執行。) 您可以手動編輯這兩個資料庫所使用的連接字串值來新增容錯移轉合作夥伴資訊。若要這樣做，請完成下列程序：

1.  使用 Internet Explorer 來開啟 **\[SQL Server Reporting Services\]** 首頁。Reporting Services 首頁 URL 包括：
    
      - **http:** 首碼。
    
      - 安裝 Reporting Services 所在電腦的完整網域名稱 (FQDN) (例如，**atl-sql-001.litwareinc.com**)。
    
      - 字元字串 **/Reports\_**。
    
      - 安裝 Monitoring Reports 所在的資料庫執行個體的名稱 (例如，**archinst**)。
    
    例如，如果 SQL Server Reporting Services 安裝在 atl-sql-001.litwareinc.com 電腦上，且 Monitoring Reports 使用資料庫執行個體 archinst，首頁 URL 看起來會像這樣：
    
    **http://atl-sql-001.litwareinc.com/Reports\_archinst**

2.  當您存取 Reporting Services 首頁之後，按一下 **\[LyncServerReports\]**，然後按一下 **\[Reports\_Content\]**。這會帶您前往 Lync Server 監視報告的 **\[Reports\_Content\]** 頁面。

3.  在 **\[Reports\_Content\]** 頁面上，按一下 **\[CDRDB\]** 資料來源。

4.  在 **\[CDRDB\]** 頁面的 **\[內容\]** 索引標籤上，尋找標示為 **\[連接字串\]** 的文字方塊。目前連接字串看起來將類似這樣：
    
    **Data source=(local)\\archinst;initial catalog=LcsCDR**

5.  編輯連接字串以包含鏡像資料庫的伺服器名稱與資料庫執行個體。例如，如果伺服器名為 atl-mirror-001 且鏡像資料庫位於 archinst 執行個體中，您將需要使用此語法新增指定鏡像資料庫：
    
    **Failover Partner=atl-mirror-001\\archinst**
    
    您所編輯的連接字串看起來將像這樣：
    
    **Data source=(local)\\archinst;Failover Partner=atl-mirror-001\\archinst;initial catalog=LcsCDR**

6.  更新連接字串之後，按一下 **\[套用\]**。

7.  在 **\[CDRDB\]** 頁面上，按一下 **\[Reports\_Content\]** 連結。按一下 **\[QMSDB\]** 資料來源，然後編輯 QoE 資料庫的連接字串。例如：
    
    **Data source=(local)\\archinst;Failover Partner=atl-mirror-001\\archinst;initial catalog=QoEMetrics**

8.  按一下 **\[套用\]**。

## 請參閱

#### 概念

[安裝 Lync Server 2013 監控報告](lync-server-2013-installing-lync-server-2013-monitoring-reports.md)  
[在 Lync Server 2013 中使用監控報告](lync-server-2013-using-monitoring-reports.md)

