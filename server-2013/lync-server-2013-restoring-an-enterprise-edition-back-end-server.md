---
title: 還原 Enterprise Edition 後端伺服器
TOCTitle: 還原 Enterprise Edition 後端伺服器
ms:assetid: 1450eb4e-3315-4d02-8f02-6e1791fb1550
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202163(v=OCS.15)
ms:contentKeyID: 52056055
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 還原 Enterprise Edition 後端伺服器

 

_**上次修改主題的時間：** 2013-02-18_

本主題說明的程序可用於下列兩種情況︰

  - 已鏡像處理之 Enterprise Edition 後端伺服器的主要和鏡像資料庫都失敗。

  - 未鏡像處理的 Enterprise Edition 後端伺服器失敗。

若您有已鏡像處理的 Enterprise Edition 後端伺服器且只有鏡像或主要資料庫失敗，請參閱＜[還原鏡像 Enterprise Edition 後端伺服器 - 主要](lync-server-2013-restoring-a-mirrored-enterprise-edition-back-end-server-primary.md)＞以還原主要資料庫，並參閱＜[還原鏡像 Enterprise Edition 後端伺服器 - 鏡像](lync-server-2013-restoring-a-mirrored-enterprise-edition-back-end-server-mirror.md)＞以還原鏡像資料庫。

若中央管理存放區失敗，請參閱＜[還原裝載中央管理存放區的伺服器](lync-server-2013-restoring-the-server-hosting-the-central-management-store.md)＞。若是非後端伺服器的 Enterprise Edition 成員伺服器失敗，請參閱＜[還原 Enterprise Edition 成員伺服器](lync-server-2013-restoring-an-enterprise-edition-member-server.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建議您在開始還原之前，先擷取系統的影像複本，以便在還原出錯時，可以利用此影像做為回復點。也建議您在安裝作業系統及 SQL Server 之後擷取影像複本，然後再還原或重新註冊憑證。</td>
</tr>
</tbody>
</table>


## 若要還原 Enterprise Edition 後端伺服器

1.  準備一部完整網域名稱 (FQDN) 與失敗電腦相同的乾淨或全新伺服器，然後安裝作業系統，再還原或重新註冊憑證。
    
    > [!NOTE]  
    > 遵循貴組織的伺服器部署程序執行此步驟。
    


2.  從 RTCUniversalServerAdmins 群組成員的使用者帳戶登入所要還原的伺服器。

3.  安裝 SQL Server 2012 或 SQL Server 2008 R2，並將執行個體名稱保持與失敗之前相同。
    
    > [!NOTE]  
    > 視您的部署而定，後端伺服器可能包含多個組合或個別的資料庫。請遵循相同程序來安裝您原本用來部署伺服器的 SQL Server，包括 SQL Server 權限和登入。
    


4.  安裝 SQL Server 之後，請執行下列動作：
    
    1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。
    
    2.  按一下 \[從現有部署下載拓撲\]，然後按一下 \[確定\]。
    
    3.  選取拓撲，然後按一下 \[儲存\]。按一下 \[是\] 確定您的選擇。
    
    4.  用滑鼠右鍵按一下 \[Lync Server 2013\] 節點，然後按一下 \[發行拓撲\]。
    
    5.  遵循 \[發行拓撲精靈\] 中的步驟。在「建立資料庫」頁面上，選取要重新建立的資料庫。
        
        > [!NOTE]  
        > 只有獨立伺服器會顯示在 [建立資料庫] 頁面上。
        
    
    6.  若要還原已鏡像處理的後端伺服器，請繼續遵循精靈中其餘的步驟，直到出現提示 \[建立鏡像資料庫\]。選取要安裝的資料庫，然後完成程序。
    
    7.  依序執行精靈中剩餘的步驟，然後按一下 \[完成\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>除了執行拓撲產生器之外，您也可以使用 <strong>Install-CsDatabase</strong> Cmdlet 建立每一個資料庫，並且使用 <strong>Install-CsMirrorDatabase</strong> Cmdlet 設定鏡像資料庫。如需詳細資訊，請參閱 Lync Server 管理命令介面文件。</td>
    </tr>
    </tbody>
    </table>


5.  執行下列動作還原使用者資料：
    
    1.  將 ExportedUserData.zip 從 $Backup\\ 複製到本機目錄。
    
    2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。
    
    3.  還原使用者資料之前，必須先停止 Lync 服務。若要執行此項作業，請輸入︰
        
            Stop-CsWindowsService
    
    4.  若要還原使用者資料，請在命令列上輸入：
        
            Import-CsUserData -PoolFqdn <Fqdn> -FileName <String>
        
        例如：
        
            Import-CsUserData -PoolFqdn "atl0cs-001.litwareinc.com" -FileName "C:\Logs\ExportedUserDatal.zip"
    
    5.  若要重新啟動 Lync 服務，請輸入︰
        
            Start-CsWindowsService

6.  若您已在此集區部署回應群組，請還原回應群組設定資料。如需詳細資訊，請參閱＜[還原回應群組設定](lync-server-2013-restoring-response-group-settings.md)＞。

7.  若您要還原的後端伺服器其中包含封存與監控資料庫，請使用 SQL Server 工具，如 SQL Server Management Studio，來還原封存與監控資料。如需詳細資訊，請參閱＜[還原監控資料和封存資料](lync-server-2013-restoring-monitoring-or-archiving-data.md)＞。

