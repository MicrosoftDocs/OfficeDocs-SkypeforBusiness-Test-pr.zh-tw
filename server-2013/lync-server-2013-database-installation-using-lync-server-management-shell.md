---
title: Lync Server 2013：使用 Lync Server 管理命令介面安裝資料庫
TOCTitle: 使用 Lync Server 管理命令介面安裝資料庫
ms:assetid: c90a6449-4dd5-4b18-b21c-ea2c2a64dc3c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398832(v=OCS.15)
ms:contentKeyID: 49292292
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中使用 Lync Server 管理命令介面安裝資料庫

 

_**上次修改主題的時間：** 2014-02-05_

將伺服器系統管理員與 SQL Server 系統管理員之間角色和責任區分開來，可能會延遲實作速度。 Lync Server 2013 使用角色存取控制 (RBAC) 來減緩這些難處。在某些情況下，SQL Server 系統管理員必須管理落在 RBAC 範圍外之 SQL Server 架構伺服器上的資料庫安裝。 Lync Server 2013 管理命令介面提供一種方法，讓 SQL Server 系統管理員能夠執行專門設計的 Windows PowerShell Cmdlet，來以正確的資料與記錄檔設定資料庫。如需詳細資訊，請參閱 [Lync Server 2013 中 SQL Server 的部署權限](lync-server-2013-deployment-permissions-for-sql-server.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>以下程序假設至少已安裝 Lync Server 2013 OCSCore.msi、SQL Server Native Client (sqlncli.msi) Microsoft SQL Server 2012 Management Objects、CLR Types for Microsoft SQL Server 2012 和 Microsoft SQL Server 2012 ADOMD.NET。OCSCore.msi 位於安裝媒體的 \Setup\AMD64\Setup 目錄。其餘元件位於 \Setup\amd64。此外，為 Lync Server 2013 準備 Active Directory 的工作也已順利完成。</td>
</tr>
</tbody>
</table>


**Install-CsDatabase** 是您用來安裝資料庫的 Windows PowerShell Cmdlet。 **Install-CsDatabase** Cmdlet 擁有大量的參數，不過本文中僅討論其中一小部分。如需有關可能參數的詳細資訊，請參閱 Lync Server 2013 管理命令介面 文件。

<table>
<thead>
<tr class="header">
<th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>為避免效能問題和可能的逾時問題發生，參考 SQL Server 架構伺服器時一定要使用完整網域名稱 (FQDN)。避免使用只有主機名稱的參考。例如，使用 sqlbe01.contoso.net，而避免使用 SQLBE01。</td>
</tr>
</tbody>
</table>


安裝資料庫時， **Install-CsDatabase** 會使用三種主要方法將資料庫放置到準備好的 SQL Server 架構伺服器上：

  - 執行 **Install-CsDatabase** 但不使用 DatabasePaths 或 UseDefaultSqlPath。Cmdlet 會使用內建的演算法判斷放置記錄和資料檔的最佳位置。演算法僅適用於獨立 SQL Server 實作。

  - 執行 **Install-CsDatabase** 並使用 DatabasePaths 參數。如果已定義 DatabasePaths 參數，則不會使用內建演算法找出記錄和資料檔的最佳位置。使用此參數可讓您定義將部署記錄和資料檔的位置。

  - 執行 **Install-CsDatabase** 並使用 UseDefaultSqlPath。此選項不會使用內建演算法找出記錄和資料檔的最佳位置。記錄和資料檔會根據 SQL Server 系統管理員設定的預設值部署。這些路徑的設定目的通常在於事先自動管理 SQL Server 上的記錄和資料檔，而與 Lync Server 2013 的安裝程式無關。

  - 您也可以使用 DatabasePathMap 參數明確指定每個資料庫和其個別記錄檔的位置。

## 使用 Windows PowerShell Cmdlet 設定 SQL Server 中央管理存放區

1.  在任何電腦上使用系統管理認證登入，以便在 SQL Server 架構伺服器上建立資料庫。如需詳細資訊，請參閱 [Lync Server 2013 中 SQL Server 的部署權限](lync-server-2013-deployment-permissions-for-sql-server.md)。

2.  開啟 Lync Server 2013 管理命令介面。如果您尚未調整 Windows PowerShell 的執行原則，則必須調整原則以便讓 Windows PowerShell 指令碼執行。如需詳細資訊，請參閱 <http://go.microsoft.com/fwlink/?linkid=203093> 的＜探討執行原則＞。

3.  使用 **Install-CsDatabase** Cmdlet 安裝 中央管理存放區。
    
      ```
      Install-CsDatabase -CentralManagementDatabase -SqlServerFqdn <fully qualified domain name of SQL Server> 
      -SqlInstanceName <named instance> -DatabasePaths <logfile path>,<database file path> 
      -Report <path to report file>
      ```
    
      ```
      Install-CsDatabase -CentralManagementDatabase -SqlServerFqdn sqlbe.contoso.net -SqlInstanceName rtc -DatabasePaths "C:\CSDB-Logs","C:\CSDB-CMS" -Report "C:\Logs\InstallDatabases.html"
      ```
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Report 參數是選用的，但是，如果您要記錄安裝程序，就會很實用。</td>
    </tr>
    </tbody>
    </table>


4.  **Install-CsDatabase –DatabasePaths** 最多可使用 6 個路徑參數，每個參數定義磁碟機的路徑，如＜SQL Server 資料和記錄檔位置＞中的定義方式。根據 Lync Server 2013 中的資料庫組態邏輯規則，磁碟機會被剖析出來並分到 2 個、4 個或 6 個「貯體」(Bucket) 中。根據您的 SQL Server 組態和貯體數目，您將提供 2 個、4 個或 6 個路徑。
    
    如果您有 3 個磁碟機，會優先散佈記錄，接著再散佈資料檔案。這裡是設定 6 個磁碟機的 SQL Server 架構伺服器的範例：
    
        Install-CsDatabase -ConfiguredDatases -SqlServerFqdn sqlbe.contoso.net -DatabasePaths "D:\CSDynLogs","E:\CSRtcLogs","F:\MonCdrArcLogs","G:\MonCdrArchData","H:\AbsAppLog","I:\DynRtcAbsAppData" -Report "C:\Logs\InstallDatabases.html"

5.  資料庫安裝完成時，您可以關閉 Lync Server 2013 管理命令介面或繼續安裝 拓撲產生器中定義的 Lync Server 2013 已設定資料庫。

## 使用 Windows PowerShell Cmdlet 設定 SQL Server 拓撲設定的資料庫

1.  若要為 Lync Server 2013 安裝 拓撲產生器設定的資料庫， Lync Server 2013 系統管理員必須發行拓撲。如需詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中發行拓撲](lync-server-2013-publish-the-topology.md)。

2.  在任何電腦上使用系統管理認證登入，以便在 SQL Server 架構伺服器上建立資料庫。請參閱 [Lync Server 2013 中 SQL Server 的部署權限](lync-server-2013-deployment-permissions-for-sql-server.md)主題。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要能夠設定 SQL Server 資料庫，請確定用來執行這裡所述步驟的 SQL Server 系統管理員帳戶，同時也是執行 SQL Server 並存放 中央管理伺服器角色之伺服器上的 sysadmins 群組成員 (或同等權限)。對於檢查需要安裝或設定 SQL Server 資料庫的任何其他 Lync Server 2013 集區而言，這個特別重要。例如，如果您要部署第二個集區 (pool02)，但是 中央管理伺服器角色是存放於 pool01。 SQL Server sysadmin 群組 (或同等權限) 必須具有這兩個 SQL Server 資料庫的權限。</td>
    </tr>
    </tbody>
    </table>


3.  開啟 Lync Server 2013 管理命令介面 (如果尚未開啟)。

4.  使用 **Install-CsDatabase** Cmdlet，安裝 拓撲產生器設定的資料庫。
    
      ```
      Install-CsDatabase -ConfiguredDatabases -SqlServerFqdn <fully qualified domain name of SQL Server> 
       -DatabasePaths <logfile path>,<database file path> -Report <path to report file>
      ```
    
      ```
      Install-CsDatabase -ConfiguredDatabases -SqlServerFqdn sqlbe.contoso.net 
       -Report "C:\Logs\InstallDatabases.html"
      ```
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Report 參數是選用的，但是，如果您要記錄安裝程序，就會很實用。</td>
    </tr>
    </tbody>
    </table>


5.  資料庫安裝完成時，關閉 Lync Server 2013 管理命令介面。

## 使用加上 DatabasePathMap 參數的 Windows PowerShell Cmdlet 來設定 SQL Server 拓撲

1.  若要安裝 Lync Server 2013 的資料庫， Lync Server 系統管理員必須建立路徑，並根據一組預先定義的規則來部署資料庫檔案和記錄檔。

2.  在任何電腦上使用系統管理認證登入，以便在 SQL Server 架構伺服器上建立資料庫。請參閱 [Lync Server 2013 中 SQL Server 的部署權限](lync-server-2013-deployment-permissions-for-sql-server.md)主題。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>為了能夠設定 SQL Server 資料庫，請確定用來執行此處所述步驟的 SQL Server 系統管理員帳戶同時也是執行 SQL Server 並存放中央管理伺服器角色之伺服器上的 sysadmins 群組成員 (或同等群組)。對於檢查需要安裝或設定 Lync Server 資料庫的任何其他 SQL Server 集區而言，這個特別重要。例如，如果您要部署第二個集區 (pool02)，但中央管理伺服器角色是存放於 pool01。SQL Server sysadmin 群組 (或同等群組) 必須具有這兩個 SQL Server 資料庫的權限。</td>
    </tr>
    </tbody>
    </table>


3.  開啟 Lync Server 管理命令介面 (如果尚未開啟)。

4.  使用加上 DatabasePathMap 參數的 **Install-CsDatabase** Cmdlet 以及 PowerShell 雜湊表來安裝 拓撲產生器設定的資料庫。

5.  在範例程式碼中，可使用 –DatabasePathsMap 參數和已定義的雜湊表來精確判定為資料庫所定義的路徑，如下所示 (在此範例中，所有資料庫 (.mdf) 檔案使用 "C:\\CSData"，所有記錄 (.ldf) 檔案則使用 "C:\\CSLogFiles"。Install-CsDatabase 會視需要建立資料夾)：
    
        $pathmap = @{
        "BackendStore:BlobStore:DbPath"="C:\CsData";"BackendStore:BlobStore:LogPath"="C:\CsLogFiles"
        "BackendStore:RtcSharedDatabase:DbPath"="C:\CsData";"BackendStore:RtcSharedDatabase:LogPath"="C:\CsLogFiles"
        "ABSStore:AbsDatabase:DbPath"="C:\CsData";"ABSStore:AbsDatabase:LogPath"="C:\CsLogFiles"
        "ApplicationStore:RgsConfigDatabase:DbPath"="C:\CsData";"ApplicationStore:RgsConfigDatabase:LogPath"="C:\CsLogFiles"
        "ApplicationStore:RgsDynDatabase:DbPath"="C:\CsData";"ApplicationStore:RgsDynDatabase:LogPath"="C:\CsLogFiles"
        "ApplicationStore:CpsDynDatabase:DbPath"="C:\CsData";"ApplicationStore:CpsDynDatabase:LogPath"="C:\CsLogFiles"
        "ArchivingStore:ArchivingDatabase:DbPath"="C:\CsData";"ArchivingStore:ArchivingDatabase:LogPath"="C:\CsLogFiles"
        "MonitoringStore:MonitoringDatabase:DbPath"="C:\CsData";"MonitoringStore:MonitoringDatabase:LogPath"="C:\CsLogFiles"
        "MonitoringStore:QoEMetricsDatabase:DbPath"="C:\CsData";"MonitoringStore:QoEMetricsDatabase:LogPath"="C:\CsLogFiles"
        }
        Install-CsDatabase -ConfigureDatabases -SqlServerFqdn sqlbe01.contoso.net -DatabasePathsMap $pathmap

6.  由於資料庫和記錄檔是以其在目的地資料庫伺服器上的位置明確地命名，您可以針對每個服務類型的實際資料庫與記錄位置來定義特定的位置。下列範例將每個特定服務類型的資料庫放在不同的磁碟上，並將關聯的記錄檔放在另一個磁碟上。例如：
    
      - 所有 RTC 資料庫放到 "D:\\RTCDatabase"
    
      - 所有 RTC 記錄檔放到 "E:\\RTCLogs"
    
      - 所有應用程式存放區資料庫放到 "F:\\CPSDatabases"
    
      - 所有應用程式存放區記錄檔放到 "G:\\CPSLogs"
    
      - 所有回應群組存放區資料庫放到 "H:\\RGSDatabases"
    
      - 所有回應群組存放區記錄檔放到 "I:\\RGSLogs"
    
      - 所有通訊錄存放區資料庫放到 "J:\\ABSDatabases"
    
      - 所有通訊錄存放區記錄檔放到 "K:\\ABSLogs"
    
      - 所有封存存放區資料庫放到 "L:\\ArchivingDatabases"
    
      - 所有封存存放區記錄檔放到 "M:\\ArchivingLogs"
    
      - 所有監控存放區資料庫放到 "N:\\MonitoringDatabases"
    
      - 所有監控存放區記錄檔放到 "O:\\MonitoringLogfiles"
    
    <!-- end list -->
    
    ``` 
    
    $pathmap = @{
    "BackendStore:BlobStore:DbPath"="D:\RTCDatabase";"BackendStore:BlobStore:LogPath"="E:\RTCLogs"
    "BackendStore:RtcSharedDatabase:DbPath"="D:\RTCDatabase";"BackendStore:RtcSharedDatabase:LogPath"="E:\RTCLogs"
    "ABSStore:AbsDatabase:DbPath"="J:\ABSDatabases";"ABSStore:AbsDatabase:LogPath"="K:\ABSLogs"
    "ApplicationStore:RgsConfigDatabase:DbPath"="H:\RGSDatabases";"ApplicationStore:RgsConfigDatabase:LogPath"="G:\CPSLogs"
    "ApplicationStore:RgsDynDatabase:DbPath"="H:\RGSDatabases";"ApplicationStore:RgsDynDatabase:LogPath"="I:\RGSLogs"
    "ApplicationStore:CpsDynDatabase:DbPath"="F:\CPSDatabases";"ApplicationStore:CpsDynDatabase:LogPath"="G:\CsLogFiles"
    "ArchivingStore:ArchivingDatabase:DbPath"="M:\ArchivingLogs";"ArchivingStore:ArchivingDatabase:LogPath"="N:\MonitoringDatabases"
    "MonitoringStore:MonitoringDatabase:DbPath"="N:\MonitoringDatabases";"MonitoringStore:MonitoringDatabase:LogPath"="O:\MonitoringLogfiles"
    "MonitoringStore:QoEMetricsDatabase:DbPath"="N:\MonitoringDatabases";"MonitoringStore:QoEMetricsDatabase:LogPath"="O:\MonitoringLogfiles"
    }
    
    Install-CsDatabase -ConfiguredDatabases -SqlServerFqdn sqlbe01.contoso.net -DatabasePathMap $pathmap
    ```
    
    使用 –DatabasePathMap 參數，您可以定義任何邏輯磁碟機代號對應組合，為您的 SQL Server 效能和位置需求提供最佳解決方案。

如果您使用 **DatabasePathMap** 方法設定資料庫資料檔案與記錄檔，則使用 拓撲產生器時將會需要對正常的程序做稍微變更。通常，您會定義拓撲選擇、發行拓撲，並選擇部署資料庫選取項目。

如果您已使用 **DatabasePathMap**，您便已經完成 拓撲產生器程序的第三部分。若是在執行 拓撲產生器之前已經有完整設定好的資料庫伺服器，您仍要定義所有的伺服器角色和選項，但是取消選取建立資料庫的選項。

