---
title: Lync Server 2013：防毒掃描排除項目
TOCTitle: Lync Server 2013 的防毒掃描排除項目
ms:assetid: 71e1f1cc-2d16-4111-9864-9276bf24dfe0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn440138(v=OCS.15)
ms:contentKeyID: 59602851
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的防毒掃描排除項目

 

_**上次修改主題的時間：** 2015-02-26_

若要確保掃毒程式不會干擾 Lync Server 2013 的運作，您必須針對會執行掃毒程式的各個 Lync Server 2013 伺服器或伺服器角色，排除特定處理序與目錄。您應排除下列處理序與目錄：

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>下方所列的資料夾與檔案位置為 Lync Server 2013 的預設位置。如您使用的任何位置並非預設值，請排除您為組織所指定的位置，而非本主題中指定的預設位置。</td>
</tr>
</tbody>
</table>


  - Lync Server 2013 處理序：
    
      - ABServer.exe
    
      - AcpMcuSvc.exe
    
      - ASMCUSvc.exe
    
      - AVMCUSvc.exe
    
      - ChannelService.exe
    
      - ClsAgent.exe
    
      - ComplianceService.exe
    
      - DataMCUSvc.exe
    
      - DataProxy.exe
    
      - FileTransferAgent.exe
    
      - IMMCUSvc.exe
    
      - LysSvc.exe
    
      - MasterReplicatorAgent.exe
    
      - MediaRelaySvc.exe
    
      - MediationServerSvc.exe
    
      - MRASSvc.exe
    
      - OcsAppServerHost.exe
    
      - ReplicaReplicatorAgent.exe
    
      - ReplicationApp.exe
    
      - RtcHost.exe
    
      - RTCSrv.exe
    
      - XmppProxy.exe
    
      - XmppTGW.exe

  - Windows Fabric 主機服務程序：
    
      - Fabric.exe
    
      - FabricDCA.exe
    
      - FabricHost.exe

  - IIS 程序：
    
      - %systemroot%\\system32\\inetsrv\\w3wp.exe
    
      - %systemroot%\\SysWOW64\\inetsrv\\w3wp.exe

  - SQL Server 後端程序：
    
      - %ProgramFiles%\\Microsoft SQL Server\\MSSQL11.MSSQLSERVER\\MSSQL\\Binn\\SQLServr.exe
    
      - %ProgramFiles%\\Microsoft SQL Server\\MSRS11.MSSQLSERVER\\Reporting Services\\ReportServer\\Bin\\ReportingServicesService.exe
    
      - %ProgramFiles%\\Microsoft SQL Server\\MSAS11.MSSQLSERVER\\OLAP\\Bin\\MSMDSrv.exe

  - SQL Server 前端程序：
    
      - %ProgramFiles%\\Microsoft SQL Server\\MSSQL11.LYNCLOCAL\\MSMQL\\Binn\\SQLServr.exe
    
      - %ProgramFiles%\\Microsoft SQL Server\\MSSQL11.RTCLOCAL\\MSMQL\\Binn\\SQLServr.exe

  - 目錄和檔案：
    
      - %systemroot%\\System32\\LogFiles
    
      - %systemroot%\\SysWow64\\LogFiles
    
      - %systemroot%\\Microsoft.NET\\assembly\\GAC\_MSIL
    
      - %programfiles%\\Microsoft Lync Server 2013
    
      - %programfiles%\\Common Files\\Microsoft Lync Server 2013\\Watcher Node
    
      - %programfiles%\\Common Files\\Microsoft Lync Server 2013
    
      - %SystemDrive%\\RtcReplicaRoot
    
      - 檔案共用存放區 (指定於拓撲產生器中)。拓撲產生器中指定了檔案存放區。
    
      - SQL Server 資料和記錄檔，包含用於後端資料庫、使用者存放區、封存存放區、監控存放區及應用程式存放區的項目。資料庫和記錄檔可在拓撲產生器中指定。如需各個資料庫的資料與記錄檔詳細資訊，包括預設名稱，請參閱部署文件中的＜ [Lync Server 2013 的 SQL Server 資料和記錄檔位置](lync-server-2013-sql-server-data-and-log-file-placement.md)＞。
    
      - SQL Server 資料與記錄檔，包括前端資料庫、Lync 存放區以及 RtcDatabase 存放區中的資料與記錄檔。這些項目通常位於 %localdrive%\\CSData。

