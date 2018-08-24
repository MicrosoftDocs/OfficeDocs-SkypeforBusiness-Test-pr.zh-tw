---
title: 還原鏡像 Enterprise Edition 後端伺服器 - 鏡像
TOCTitle: 還原鏡像 Enterprise Edition 後端伺服器 - 鏡像
ms:assetid: 4b3c8eae-6f1f-4377-b39b-6699e725c517
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945626(v=OCS.15)
ms:contentKeyID: 52056102
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 還原鏡像 Enterprise Edition 後端伺服器 - 鏡像

 

_**上次修改主題的時間：** 2013-02-19_

若您的 Enterprise Edition 後端伺服器為鏡像組態，且只有鏡像失敗，請遵循本節中的程序。若主要資料庫和鏡像都失敗，請參閱＜[還原 Enterprise Edition 後端伺服器](lync-server-2013-restoring-an-enterprise-edition-back-end-server.md)＞。若只有主要資料庫失敗，請參閱＜[還原鏡像 Enterprise Edition 後端伺服器 - 主要](lync-server-2013-restoring-a-mirrored-enterprise-edition-back-end-server-primary.md)＞。若裝載中央管理存放區的資料庫失敗，請參閱＜[還原裝載中央管理存放區的伺服器](lync-server-2013-restoring-the-server-hosting-the-central-management-store.md)＞。若是非後端伺服器的 Enterprise Edition 成員伺服器失敗，請參閱＜[還原 Enterprise Edition 成員伺服器](lync-server-2013-restoring-an-enterprise-edition-member-server.md)＞。

建議您在開始還原之前，先擷取系統的影像複本，以便在還原出錯時，可以利用此影像做為回復點。也建議您在安裝作業系統及 SQL Server，並還原或重新註冊憑證之後，再擷取影像複本。

## 還原 Enterprise Edition 後端伺服器鏡像資料庫

1.  以 RTCUniversalServerAdmins 群組成員的使用者帳戶登入至前端伺服器。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  解除安裝鏡像。首先，輸入下列 Cmdlet︰
    
        Uninstall -CsMirrorDatabase -DatabaseType User -SqlServerFqdn <PrimaryServerFqdn> -SqlInstanceName <SQLInstance> -verbose
    
    例如︰
    
        Uninstall -CsMirrorDatabase -DatabaseType User -SqlServerFqdn server4.contoso.com -SqlInstanceName archinst -verbose
    
    針對此伺服器上所有的資料庫類型執行此作業。

4.  建立一部其完整網域名稱 (FQDN) 與失敗電腦相同 (DB1.contoso.com) 的乾淨或全新伺服器，然後安裝作業系統，再還原或重新註冊憑證。此伺服器會以新鏡像的身分運作。

5.  以 RTCUniversalServerAdmins 群組成員的使用者帳戶登入至新伺服器。

6.  安裝 SQL Server 2012 或 SQL Server 2008 R2，並將執行個體名稱保持與失敗之前相同。

7.  以 RTCUniversalServerAdmins 群組成員的使用者帳戶登入至前端伺服器。

8.  使用拓撲產生器來安裝鏡像資料庫。請執行下列動作︰
    
      - 啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。
    
      - 以滑鼠右鍵按一下 Lync Server 2013 節點，按一下 \[拓撲\]，然後按一下 \[安裝資料庫\]。
    
      - 遵循 \[安裝資料庫精靈\] 中的步驟。在「建立資料庫」頁面上，選取要重新建立的資料庫。
    
      - 遵循精靈中的步驟，直到系統提示 \[建立鏡像資料庫\]。選取要安裝的資料庫，然後完成程序。
        
        > [!TIP]  
        > 除了執行拓撲產生器之外，也可以使用 <strong>Install-CsMirrorDatabase</strong> Cmdlet 來設定鏡像。如需詳細資訊，請參閱 Lync Server 管理命令介面文件。

