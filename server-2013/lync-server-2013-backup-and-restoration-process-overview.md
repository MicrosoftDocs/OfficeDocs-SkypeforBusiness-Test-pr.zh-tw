---
title: 備份和還原程序概觀
TOCTitle: 備份和還原程序概觀
ms:assetid: e0f23b21-070f-4df5-b795-cea2f5338d85
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202192(v=OCS.15)
ms:contentKeyID: 52056237
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 備份和還原程序概觀

 

_**上次修改主題的時間：** 2013-03-26_

本節提供適用於 Lync Server 2013 的備份與還原程序方法概觀。不論位置為何，所有的 Standard Edition Server 及 Enterprise Edition Server 都使用相同的程序。

一般來說，備份程序的運作方式如下：

  - 建立一個備份位置，作為獨立電腦 (不是任何集區的一部分) 上的共用資料夾。備份位置以 **$Backup** 表示。

  - 以固定的排程時間，遵循＜[備份 Lync Server](lync-server-2013-backing-up-lync-server.md)＞中所述之程序，備份所有 Lync Server 資料庫以及＜[備份和還原需求：資料](lync-server-2013-backup-and-restoration-requirements-data.md)＞中所述的所有檔案存放區。中央管理存放區包含所有伺服器設定及配置。

  - 每次執行後續備份時，就會建立新的共用資料夾，同時會變更 **$Backup** 參照的路徑。

一般來說，還原程序的運作方式如下：

  - 發生失敗或中斷時，請將 **$Backup** 所參照之位置內的資料，還原至全新或乾淨的電腦。
    
    > [!IMPORTANT]  
    > 此還原處理作業並不會將資料還原至現有的伺服器狀態。也就是說，此處理作業需要伺服器是乾淨或新的伺服器。
    


  - 若要讓您的使用者和會議資訊可復原至失敗點，您可以在配對前端集區實作災難復原拓撲，如＜[在 Lync Server 2013 中規劃高可用性和災害復原](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)＞中所述。除此之外，Lync Server 僅可對其資料庫支援簡單復原模式。透過簡單復原模式，可將資料庫復原至上次的完整備份點，表示您無法將資料庫還原至失敗點或特定時間點。對許多組織而言，簡單復原模式是最佳選擇，因為 Lync Server 後端資料庫 (RTCXDS.mdf) 實際上比交易記錄檔更小，而且比一般企業營運資料庫應用程式明顯較小。

  - 所有的網域名稱系統 (DNS) 設定、動態主機設定通訊協定 (DHCP) 設定、網域名稱、電腦的完整網域名稱 (FQDN)、檔案存放區路徑等等，在備份當時的還原時都必須相同。

若執行 Lync Server 的伺服器失敗，復原作業包含下列步驟：

  - 在和失敗的電腦具有相同 FQDN 的新電腦或乾淨電腦上，安裝作業系統。

  - 重新安裝憑證。

  - 若該伺服器主控資料庫，請安裝 Microsoft SQL Server 2012 或 Microsoft SQL Server 2008 R2。

  - 一般來說，若該伺服器主控資料庫，請執行拓撲產生器建立並安裝資料庫，並設定存取控制清單 (ACL)。

  - 一般來說，若該伺服器主控伺服器角色，請執行 Lync Server 部署精靈的步驟 1 到步驟 4，安裝本機設定檔、安裝伺服器角色元件，指派憑證，並啟動服務。
    
    > [!NOTE]  
    > 若該伺服器主控組合有伺服器角色的資料庫，請執行 Lync Server 部署精靈的步驟 2，重建資料庫。
    


  - 若該伺服器主控資料庫，請還原備份資料。

