---
title: Lync Server 2013：設定主要鏡像與記錄傳送次要資料庫之間的 SQL Server 記錄傳送
TOCTitle: 設定主要鏡像與記錄傳送次要資料庫之間的 SQL Server 記錄傳送
ms:assetid: 4e8e9ce9-4301-47f2-a0c3-669afeb53295
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204887(v=OCS.15)
ms:contentKeyID: 49290873
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定主要鏡像與記錄傳送次要資料庫之間的 SQL Server 記錄傳送

 

_**上次修改主題的時間：** 2013-02-21_

如果主要 常設聊天室資料庫容錯移轉至其鏡像資料庫，請執行下列步驟以繼續進行記錄傳送。

1.  將主要 常設聊天室資料庫以手動方式容錯移轉至鏡像。這可以透過使用 Lync Server 管理命令介面和 **Invoke-CsDatabaseFailover** Cmdlet 來完成。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中針對後端伺服器高可用性部署 SQL 鏡像](lync-server-2013-deploying-sql-mirroring-for-back-end-server-high-availability.md)＞中的＜使用 Lync Server 管理命令介面 Cmdlet＞。

2.  使用 SQL Server Management Studio，連接至主要 常設聊天室伺服器 鏡像執行個體。

3.  確定 SQL Server Agent 執行中。

4.  以滑鼠右鍵按一下 mgc 資料庫，然後按一下 \[內容\] 。

5.  在 \[選取頁面\] 底下，按一下 \[交易記錄傳送\] 。

6.  選取 \[將此啟用為記錄傳送組態的主要資料庫\] 核取方塊。

7.  在 \[交易記錄備份\] 底下，按一下 \[備份設定\] 。

8.  在 **\[備份資料夾的網路路徑\]** 方塊中，鍵入您為異動記錄備份資料夾所建立的共用的網路路徑。

9.  如果備份資料夾位在主要伺服器上，請在 \[如果備份資料夾位於主要伺服器上，請輸入至該資料夾的本機路徑 (範例: c:\\backup):\] 方塊中輸入備份資料夾的本機路徑。(如果備份資料夾不在主要伺服器上，可將此方塊保留空白。)
    
    > [!IMPORTANT]  
    > 如果主要伺服器上的 SQL Server 服務帳戶是在本機系統帳戶之下執行，則必須在主要伺服器上建立備份資料夾，並指定該資料夾的本機路徑。
    


10. 設定 \[指定刪除檔案的時限\] 及 \[如果未在此時間內進行備份，則發出警示\] 參數。

11. 查看列在 **\[備份作業\]** 下的 **\[排程\]** 方塊中的備份排程。如果要自訂安裝排程，按一下 **\[排程\]** ，然後依需要調整 SQL Server Agent 排程。
    
    > [!IMPORTANT]  
    > 使用和主要資料庫相同的設定。
    


12. 在 **\[壓縮\]** 下，選取 **\[使用預設伺服器設定\]** ，然後按一下 **\[確定\]** 。

13. 在 \[次要伺服器執行個體與資料庫\] 底下，按一下 \[新增\] 。

14. 按一下 **\[連線\]** ，然後連線至您已設定為次要伺服器的 SQL Server 的執行個體。

15. 在 \[次要資料庫\] 方塊中，從清單選取 \[mgc\] 資料庫。

16. 在 **\[初始化次要資料庫\]** 索引標籤上，選取選項 **\[否，次要資料庫已初始化\]** 。

17. 在 **\[複製檔案\]** 索引標籤的 **\[複製之檔案的目的資料夾\]** 中，鍵入應複製異動記錄備份的資料夾的路徑，然後按一下 **\[確定\]** 。這個資料夾通常位於次要伺服器上。

18. 開啟 **\[指令碼設定\]** 下拉式清單，然後選取 **\[編寫組態的指令碼至新增查詢視窗\]** 。

19. 在新增查詢視窗的 **\[資料庫屬性\]** 中，按一下 **\[確定\]** 開始設定程序。

20. 選取並執行前半部的查詢 (請參閱步驟 18) 直到此行：\*\*\*\*\*\* End: Script to be run at Primary: \*\*\*\*\*\*。
    
    > [!IMPORTANT]  
    > 您必須手動執行此指令碼，因為 SQL Server Management Studio 在 SQL Server 記錄傳送設定中不支援多個主要資料庫。
    


21. 選取 **\[取消\]** 以關閉記錄檔傳送設定面板，然後建立工作設定，正確實作主要和鏡像資料庫 (若容錯移轉) 的記錄檔傳送。

22. 以手動方式將主要 常設聊天室資料庫容錯回復至主要資料庫。這可以透過使用 Lync Server 管理命令介面和 **Invoke-CsDatabaseFailover** Cmdlet 來完成。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中針對後端伺服器高可用性部署 SQL 鏡像](lync-server-2013-deploying-sql-mirroring-for-back-end-server-high-availability.md)＞中的＜使用 Lync Server 管理命令介面 Cmdlet＞。

## 請參閱

#### 概念

[在 Lync Server 2013 中針對後端伺服器高可用性部署 SQL 鏡像](lync-server-2013-deploying-sql-mirroring-for-back-end-server-high-availability.md)  
[在 Lync Server 2013 中針對後端伺服器高可用性部署 SQL 鏡像](lync-server-2013-deploying-sql-mirroring-for-back-end-server-high-availability.md)

