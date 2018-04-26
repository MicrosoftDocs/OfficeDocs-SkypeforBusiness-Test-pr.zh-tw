---
title: 在 Lync Server 2013 中升級或更新後端伺服器或 Standard Edition Server
TOCTitle: 在 Lync Server 2013 中升級或更新後端伺服器或 Standard Edition Server
ms:assetid: f95f8d3a-e039-484e-97bd-d727db21a12b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721942(v=OCS.15)
ms:contentKeyID: 49890514
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中升級或更新後端伺服器或 Standard Edition Server

 

_**上次修改主題的時間：** 2012-11-01_

本節說明如何在 Enterprise Edition後端伺服器 或 Standard Edition 伺服器上安裝更新。

如果後端伺服器在升級時停機超過 30 分鐘，則使用者會進入復原模式。升級完成時，後端伺服器會再次與集區中的前端伺服器連線，使用者可恢復使用完整功能。如果升級時間未超過 30 分鐘，則不會影響使用者。

## 更新後端伺服器或 Standard Edition Server

1.  以 CsAdministrator 角色成員身分登入您要升級的伺服器。

2.  下載更新並解壓縮至本機硬碟機。

3.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[程式集\]、\[Microsoft Lync Server 2013\] 以及 \[Lync Server 管理命令介面\]。

4.  停止 Lync Server 服務。在命令列中輸入：
    
        Stop-CsWindowsService

5.  停止全球資訊網服務。在命令列中輸入：
    
        net stop w3svc

6.  關閉所有 Lync Server 管理命令介面視窗。

7.  安裝更新。

8.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[程式集\]、\[Microsoft Lync Server 2013\] 以及 \[Lync Server 管理命令介面\]。

9.  再次停止 Lync Server服務，以取得全域組件快取 (GAC) –d 組件。在命令列中輸入：
    
        Stop-CsWindowsService

10. 重新啟動全球資訊網服務。在命令列中輸入：
    
        net start w3svc

11. 執行下列其中一項，將 LyncServerUpdateInstaller.exe 所做的變更套用至 SQL Server 資料庫：
    
      - 如果這是 Enterprise Edition後端伺服器 且這部伺服器上沒有組合的資料庫，例如「封存」或「監控」資料庫，則請在命令列中輸入下列命令：
        
            Install-CsDatabase -Update -ConfiguredDatabases -SqlServerFqdn <SQL Server FQDN>
    
      - 如果這是 Enterprise Edition後端伺服器 且這部伺服器上有組合的資料庫，則請在命令列中輸入下列命令：
        
            Install-CsDatabase -Update -ConfiguredDatabases -SqlServerFqdn <SQL Server FQDN>  -ExcludeCollocatedStores
    
      - 如果這是 Standard Edition 伺服器，請在命令列中輸入下列命令：
        
            Install-CsDatabase -Update -LocalDatabases

