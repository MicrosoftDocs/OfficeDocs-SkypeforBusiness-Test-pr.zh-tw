---
title: Lync Server 2013：容錯移轉常設聊天室伺服器
TOCTitle: 容錯移轉常設聊天室伺服器
ms:assetid: 2cd79ffd-fee6-44ce-96cf-b98bf25e2690
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204772(v=OCS.15)
ms:contentKeyID: 49290451
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中容錯移轉常設聊天室伺服器

 

_**上次修改主題的時間：** 2014-02-05_

常設聊天室伺服器 的容錯移轉設計主要是作為手動程序。

容錯移轉程序是假設啟用及執行了次要資料中心，卻完全無法使用 常設聊天室資料庫所在的 常設聊天室伺服器 服務，包含：

  - 常設聊天室伺服器 主要資料庫及 常設聊天室伺服器 鏡像資料庫已關閉。

  - Lync Server前端伺服器已關閉。

此程序主要有兩個基本步驟：

  - 復原主要 常設聊天室 資料庫 (mgc)。

  - 建立新主要資料庫的鏡像。

常設聊天室 規範資料庫 (mgccomp) 並無容錯移轉。此資料庫的內容僅為暫時性，且會在規範介面卡處理資料時被清除。身為 常設聊天室 管理員，您有責任要正確地管理介面卡輸出以避免資料遺失。

## 容錯移轉 常設聊天室伺服器

1.  從 常設聊天室伺服器 備份記錄傳送資料庫移除記錄傳送。
    
    1.  使用 SQL Server Management Studio 連線至 常設聊天室伺服器 備份 mgc 資料庫所在的資料庫執行個體。
    
    2.  開啟 Master 資料庫的查詢視窗。
    
    3.  使用下列命令移除記錄傳送：
        
            exec sp_delete_log_shipping_secondary_database mgc

2.  從備份共用複製所有未複製的備份檔案至備份伺服器的複製目的地資料夾。

3.  依序將所有未套用的交易記錄備份套用至次要資料庫。如需詳細資訊，請參閱＜如何：套用交易記錄備份 (Transact-SQL)＞，網址為 http://go.microsoft.com/fwlink/?linkid=247428\&clcid=0x404

4.  若要使備份 mgc 資料庫上線。請使用步驟 1b 中開啟的查詢視窗，執行下列動作：
    
    1.  結束所有 mgc 資料庫的連線 (若有連線)：
        
        1.  **exec sp\_who2** 識別 mgc 資料庫的連線。
        
        2.  **kill \<spid\>** 結束這些連線。
    
    2.  使資料庫上線：
        
        1.  **使用復原來還原資料庫 mgc** 。

5.  在 Lync Server 管理命令介面中，使用 **Set-CsPersistentChatState -Identity "service:atl-cs-001.litwareinc.com" –PoolState FailedOver** 命令來容錯移轉至 mgc 備份資料庫。請務必針對 atl-cs-001.litwareinc.com 取代常設聊天室集區的完整網域名稱。
    
    現在 mgc 備份資料庫已是主要資料庫。

6.  在 Lync Server 管理命令介面中，使用 **Install-CsMirrorDatabase** Cmdlet 建立已是主要資料庫之備份資料庫的高可用性鏡像。使用備份資料庫執行個體作為主要資料庫，而使用備份鏡像資料庫執行個體作為鏡像執行個體。此鏡像並不是安裝程式期間，最初為主要資料庫設定的鏡像。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中針對後端伺服器高可用性部署 SQL 鏡像](lync-server-2013-deploying-sql-mirroring-for-back-end-server-high-availability.md)＞中的＜使用 Lync Server 管理命令介面 Cmdlet＞。

7.  將 常設聊天室伺服器 設為動態伺服器。從 Lync Server 命令殼層使用 **Set-CsPersistentChatActiveServer** Cmdlet 設定動態伺服器的清單。
    
    > [!IMPORTANT]  
    > 所有作用中的伺服器必須位於與新主要資料庫相同的資料中心，或位於具有低延遲/高頻寬資料庫連線的資料中心內。
    
    
    此時從 常設聊天室伺服器 主要資料庫到 常設聊天室伺服器 備份資料庫的容錯移轉即可成功完成。

