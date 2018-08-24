---
title: 還原鏡像 Enterprise Edition 後端伺服器 - 主要
TOCTitle: 還原鏡像 Enterprise Edition 後端伺服器 - 主要
ms:assetid: bc555b46-70c5-4eee-ae91-e195df238293
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945648(v=OCS.15)
ms:contentKeyID: 52056214
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 還原鏡像 Enterprise Edition 後端伺服器 - 主要

 

_**上次修改主題的時間：** 2013-02-17_

如果您在鏡像組態中有一部 Enterprise Edition 後端伺服器，而且只有主要的資料庫裝置發生故障，請遵循本節的程序；如果主要的資料庫和鏡像裝置均發生故障，請參閱＜[還原 Enterprise Edition 後端伺服器](lync-server-2013-restoring-an-enterprise-edition-back-end-server.md)＞。若只有鏡像裝置發生故障，請參閱＜[還原鏡像 Enterprise Edition 後端伺服器 - 鏡像](lync-server-2013-restoring-a-mirrored-enterprise-edition-back-end-server-mirror.md)＞。若託管中央管理存放區的資料庫裝置發生故障，請參閱＜[還原裝載中央管理存放區的伺服器](lync-server-2013-restoring-the-server-hosting-the-central-management-store.md)＞。若 Enterprise Edition 成員伺服器 (非為後端伺服器) 發生故障，請參閱＜[還原 Enterprise Edition 成員伺服器](lync-server-2013-restoring-an-enterprise-edition-member-server.md)＞。

建議您在開始還原之前先複製系統影像。在還原期間發生錯誤時，您可以將此影像當作回復點使用。您可能想要在安裝作業系統和 SQL Server 之後進行影像複製，再還原或重新註冊憑證。

在本主題中，主要資料庫範例會有完整網域名稱 (FQDN)，名稱為 BE1.contoso.com，而鏡像資料庫的 FQDN 為 BE2.contoso.com。

## 還原 Enterprise Edition 後端伺服器主要資料庫

1.  以 RTCUniversalServerAdmins 群組成員的使用者帳戶登入至前端伺服器。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  強制所有已設定的資料庫容錯移轉至鏡像資料庫。針對每個您已在此伺服器上設定的資料庫類型，輸入下列 Cmdlet：
    
        Invoke-CsDataBaseFailover -PoolFqdn <Pool FQDN> -DatabaseType <Configured Database Type> -NewPrincipal Mirror -Force -Verbose
    
    例如：
    
        Invoke-CsDataBaseFailover -PoolFqdn pool0.vdomain.com -DatabaseType User -NewPrincipal Mirror -Force -Verbose
    
    > [!WARNING]
    > 如果您已將後端資料庫設定為使用具有見證的同步鏡像，將自動進行容錯移轉。


4.  完成容錯移轉後，執行下列作業：
    
      - 啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。
    
      - 停用後端伺服器上的鏡像：以滑鼠按一下 \[Enterprise Edition 前端伺服器集區\] 下的集區並選取 \[編輯內容\]。在 \[一般\] 索引標籤的 \[關聯\] 下，取消選取 \[啟用 SQL Server 存放區鏡像\] 核取方塊。視需要針對封存和監控執行此項作業。然後按一下 \[確定\]。
    
      - 以滑鼠右鍵按一下 Lync Server 2013 節點，按一下 \[拓撲\]，然後按一下 \[發行\]。
    
      - 選取仍在運作的後端 (BE2.contoso.com)，將其做為新的 SQL 存放區。如要執行此作業，以滑鼠按一下 \[Enterprise Edition 前端集區\] 下的集區並選取 \[編輯內容\]。在 \[一般\] 索引標籤的 \[關聯\] 下，輸入 \[SQL Server 存放區\] 欄位中正在運作之後端的 FQDN (以我們的範例，名稱為 BE2.contoso.com)。
    
      - 以滑鼠右鍵按一下 Lync Server 2013 節點，按一下 \[拓撲\]，然後按一下 \[發行\]。
    
      - 重新啟動服務以便每部伺服器可以讀取新的拓撲。從 Lync Server 管理命令介面，在屬於此集區的每部前端伺服器上執行下列 Cmdlet：
        
            Stop-CsWindowsService
            Start-CsWindowsService

5.  解除安裝鏡像。從 Lync Server 管理命令介面，執行下列 Cmdlet：
    
        Uninstall-CsMirrorDatabase -DatabaseType User -SqlServerFqdn <MirrorServerFqdn> -SqlInstanceName <SQLInstance> -verbose
    
    例如：
    
        Uninstall-CsMirrorDatabase -DatabaseType User -SqlServerFqdn DB2.contoso.com -SqlInstanceName rtc -verbose
    
    針對此伺服器上所有的資料庫類型執行此作業。

6.  像故障的電腦一樣建立具有相同 FQDN 的乾淨或全新伺服器 (在此範例中，名稱為 DB1.contoso.com)，安裝作業系統，然後還原或重新註冊憑證。此伺服器會以新鏡像的身分運作。

7.  以 RTCUniversalServerAdmins 群組成員的使用者帳戶登入至新伺服器。

8.  安裝 SQL Server 2012 或 SQL Server 2008 R2，並將執行個體名稱保持與失敗之前相同。

9.  以 RTCUniversalServerAdmins 群組成員的使用者帳戶登入至前端伺服器。

10. 使用拓撲產生器安裝鏡像 DB。請執行下列步驟：
    
      - 啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。
    
      - 啟用後端伺服器上的鏡像。若要執行此作業，以滑鼠右鍵按一下 \[Enterprise Edition 前端集區\] 下的集區並選取 \[編輯內容\]。在 \[一般\] 索引標籤的 \[關聯\] 下，選取 \[啟用 SQL Server 存放區鏡像\] 核取方塊。亦可視需要針對封存和監控執行此項作業。
        
        然後，在 \[鏡像 SQL Server 存放區\] 欄位，輸入新伺服器的 FQDN (在此範例中，名稱為 BE1.contoso.com)。然後按一下 \[確定\]。
    
      - 以滑鼠右鍵按一下 Lync Server 2013 節點，按一下 \[拓撲\]，然後按一下 \[安裝資料庫\]。
    
      - 遵循 \[安裝資料庫精靈\] 中的步驟。在「建立資料庫」頁面上，選取要重新建立的資料庫。
    
      - 遵循精靈的步驟，直到系統出現 \[建立鏡像資料庫\] 提示。選取要安裝的資料庫並完成此程序。

