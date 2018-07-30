---
title: 還原裝載中央管理存放區的伺服器
TOCTitle: 還原裝載中央管理存放區的伺服器
ms:assetid: 3bd6c82c-07fb-4798-b8f9-e7c78a5a83d5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202172(v=OCS.15)
ms:contentKeyID: 52056087
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 還原裝載中央管理存放區的伺服器

 

_**上次修改主題的時間：** 2013-02-21_

Lync Server 部署有單一中央管理存放區，其複本會複寫至每部執行 Lync Server 伺服器角色的伺服器。本節說明如何還原主控中央管理存放區的後端伺服器或 Standard Edition 伺服器。

若要尋找中央管理伺服器所在的集區，請開啟拓撲產生器，按一下 \[Lync Server\]，然後查看 \[中央管理伺服器\] 底下的右窗格。

如果主控中央管理存放區的後端伺服器經過鏡像設定，且鏡像資料庫仍可運作，則建議您將此仍可運作的鏡像加以備份，然後使用此備份並遵循下列的還原程序，對主要資料庫和鏡像資料庫執行完整還原。這是必要的，因為後端還原需要修改及發行拓撲，而這只有在主控 CMS 的主要資料庫仍可操作時才可執行。此外，如果拓撲無法發行，則主要資料庫和鏡像資料庫角色無法互換。

> [!NOTE]  
> 如果並未主控中央管理存放區的後端伺服器或 Standard Edition 伺服器失敗，請參閱＜<a href="lync-server-2013-restoring-an-enterprise-edition-back-end-server.md">還原 Enterprise Edition 後端伺服器</a>＞或＜<a href="lync-server-2013-restoring-a-standard-edition-server.md">還原 Standard Edition 伺服器</a>＞。如果主控中央管理存放區的後端伺服器經過鏡像設定，且只有鏡像失敗，請參閱＜<a href="lync-server-2013-restoring-a-mirrored-enterprise-edition-back-end-server-mirror.md">還原鏡像 Enterprise Edition 後端伺服器 - 鏡像</a>＞。如果是任何其他伺服器失敗，請參閱＜<a href="lync-server-2013-restoring-an-enterprise-edition-member-server.md">還原 Enterprise Edition 成員伺服器</a>＞。



> [!TIP]
> 建議您在開始還原之前，先擷取系統的影像複本，以便在還原出錯時，可以利用此影像做為回復點。也建議您在安裝作業系統及 SQL Server 之後擷取影像複本，然後再還原或重新註冊憑證。


## 還原中央管理存放區

1.  準備一部完整網域名稱 (FQDN) 與失敗電腦相同的乾淨或全新伺服器，然後安裝作業系統，再還原或重新註冊憑證。
    
    > [!NOTE]  
    > 遵循貴組織的伺服器部署程序執行此步驟。
    


2.  從 RTCUniversalServerAdmins 群組成員和本機系統管理員群組成員的使用者帳戶，登入所要還原的伺服器。

3.  如果您要還原 Standard Edition 伺服器，請從 $Backup 將適當的檔案存放區複製到伺服器上的檔案存放區位置，以還原檔案存放區，然後共用資料夾。
    
    > [!IMPORTANT]  
    > 還原後之檔案存放區的路徑與檔案名稱應與檔案存放區備份完全相同，如此使用該檔案的元件才可存取使用。
    


4.  執行下列其中一項作業：
    
      - 如果您要安裝 Standard Edition 伺服器，請瀏覽至 Lync Server 安裝資料夾或媒體，然後啟動位在 \\setup\\amd64\\Setup.exe 的 \[Lync Server 部署精靈\]。在 \[部署精靈\] 中，按一下 \[準備第一個 Standard Edition Server\]，然後遵循精靈的指示安裝中央管理存放區。
    
      - 如果您要安裝 Enterprise 後端伺服器，請安裝 SQL Server 2012 或 SQL Server 2008 R2，並保留失敗之前的執行個體名稱。
        
        > [!NOTE]  
        > 依據您要還原的伺服器以及您的部署，伺服器可能包含多個組合或分開的資料庫。請遵循您原先用來部署伺服器的相同程序來安裝 SQL Server，包括 SQL Server 權限及登入。
        


5.  從前端伺服器，啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

6.  重新建立中央管理存放區。在命令列中輸入：
    
        Install-CsDatabase -CentralManagementDatabase -Clean -SqlServerFqdn <FQDN> -SqlInstanceName <instance name> -Verbose
    
    例如：
    
        Install-CsDatabase -CentralManagementDatabase -Clean -SqlServerFqdn Server01.contoso.com -SqlInstanceName cms -Verbose

7.  設定中央管理存放區的 Active Directory 網域服務 控制點。在命令列中輸入：
    
        Set-CsConfigurationStoreLocation -SqlServerFqdn <FQDN> -SqlInstanceName <instance name> -Verbose
    
    例如：
    
        Set-CsConfigurationStoreLocation -SqlServerFqdn Server01.contoso.com -SqlInstanceName cms -Verbose
    
    > [!NOTE]  
    > 如果您遺失連線點，可以重新執行此 Cmdlet。
    


8.  從 $Backup 匯入中央管理存放區資料。在命令列中輸入：
    
        Import-CsConfiguration -FileName <CMS backup file name>
    
    例如：
    
        Import-CsConfiguration -FileName "C:\Config.zip"

9.  啟用您剛才進行的變更。在命令列中輸入：
    
        Enable-CsTopology
    
    > [!NOTE]  
    > 啟用拓撲之後，即可在資料庫中找到拓撲文件。
    


10. 如果您要還原也有主控 CMS 的 Enterprise Edition後端伺服器，或如果需要重新建立 CMS 的鏡像，請遵循此步驟。否則，請跳至步驟 11。
    
    執行下列動作以安裝獨立資料庫：
    
    1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。
    
    2.  按一下 \[從現有部署下載拓撲\]，然後按一下 \[確定\]。
    
    3.  選取拓撲，然後按一下 \[儲存\]。按一下 \[是\] 確定您的選擇。
    
    4.  用滑鼠右鍵按一下 \[Lync Server 2013\] 節點，然後按一下 \[安裝資料庫\]。
    
    5.  遵循 \[安裝資料庫精靈\] 中的步驟。如果您要還原的資料庫不是此伺服器上的中央管理存放區，請在「建立資料庫」頁面上，選取要重新建立的資料庫。
        
        > [!NOTE]  
        > 只有獨立資料庫會顯示在「建立資料庫」頁面上。組合資料庫會在您執行 [Lync Server 部署精靈] 時建立。
        
    
    6.  如果您要還原經過鏡像處理的後端伺服器，請繼續遵循精靈中的其餘步驟，直到出現 \[建立鏡像資料庫\] 提示。選取要安裝的資料庫，然後完成程序。
    
    7.  依序執行精靈中剩餘的步驟，然後按一下 \[完成\]。
    
    > [!TIP]
    > 除了執行拓撲產生器之外，您也可以使用 <strong>Install-CsDatabase</strong> Cmdlet 建立每一個資料庫，並且使用 <strong>Install-CsMirrorDatabase</strong> Cmdlet 設定鏡像資料庫。如需詳細資訊，請參閱＜<a href="https://docs.microsoft.com/en-us/powershell/module/skype/Install-CsDatabase">Install-CsDatabase</a>＞和＜<a href="https://docs.microsoft.com/en-us/powershell/module/skype/Install-CsMirrorDatabase">Install-CsMirrorDatabase</a>＞。


11. 如果您要還原Standard Edition 伺服器，請瀏覽至 Lync Server 安裝資料夾或媒體，然後啟動位在 \\setup\\amd64\\Setup.exe 的 \[Lync Server 部署精靈\]。使用 \[Lync Server 部署精靈\] 來執行下列動作：
    
    1.  執行 \[步驟 1: 安裝本機組態存放區\]，以安裝本機設定檔。
    
    2.  執行 \[步驟 2: 設定或移除 Lync Server 元件\]，以安裝 Lync Server 伺服器角色。
    
    3.  執行 \[步驟 3: 要求、安裝或指派憑證\]，以指派憑證。
    
    4.  執行 \[步驟 4: 啟動服務\]，以啟動伺服器上的服務。
    
    如需執行 \[部署精靈\] 的詳細資訊，請參閱您要還原之伺服器角色的部署文件。

12. 執行下列動作還原使用者資料：
    
    1.  將 ExportedUserData.zip 從 $Backup\\ 複製到本機目錄。
    
    2.  還原使用者資料之前，必須先停止 Lync 服務。若要執行此項作業，請輸入：
        
            Stop-CsWindowsService
    
    3.  若要還原使用者資料，請在命令列上輸入：
        
            Import-CsUserData -PoolFqdn <Fqdn> -FileName <String>
        
        例如：
        
            Import-CsUserData -PoolFqdn "atl0cs-001.litwareinc.com" -FileName "C:\Logs\ExportedUserDatal.zip"
    
    4.  若要重新啟動 Lync 服務，請輸入︰
        
            Start-CsWindowsService

13. 將位置資訊資料還原至中央管理存放區。在命令列中輸入：
    
        Import-CsLisConfiguration -FileName <LIS backup file name>
    
    例如：
    
        Import-CsLisConfiguration -FileName "D:\E911Config.zip"

14. 如果您已在此集區或 Standard Edition 伺服器 上部署回應群組，請還原回應群組設定資料。如需詳細資訊，請參閱＜[還原回應群組設定](lync-server-2013-restoring-response-group-settings.md)＞。

15. 如果您要還原包含封存或監控資料庫的後端伺服器，請使用 SQL Server 管理工具 (如 SQL Server Management Studio) 來還原封存或監控資料。如需詳細資訊，請參閱＜[還原監控資料和封存資料](lync-server-2013-restoring-monitoring-or-archiving-data.md)＞。

