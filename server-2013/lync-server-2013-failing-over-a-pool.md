---
title: Lync Server 2013：容錯移轉集區
TOCTitle: 容錯移轉集區
ms:assetid: 10b13732-bc80-4cb2-a71c-56b1d6cb5bbb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204678(v=OCS.15)
ms:contentKeyID: 49290122
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中容錯移轉集區

 

_**上次修改主題的時間：** 2014-10-10_

如果單一前端集區失敗，而需要容錯移轉，請使用下列程序。在此程序中，Datacenter1 包含 Pool1，而 Pool1 失敗了。您要容錯移轉至位在 Datacenter2 的 Pool2。

集區容錯移轉大部分的工作都和容錯移轉 中央管理存放區有關 (若有需要的話)。這很重要，因為當集區的使用者容錯移轉時， 中央管理存放區必須可運作。

此外，如果前端集區失敗，但位在該網站的 Edge 集區仍在執行中，您就必須知道 Edge 集區是否使用失敗的集區作為下一個躍點集區。如果是，則必須先變更 Edge 集區為使用不同的前端集區，再容錯移轉至失敗的前端集區。變更下一個躍點設定的方式，取決於 Edge 將要使用的集區是位在與 Edge 集區相同的網站，還是不同網站。

**將 Edge 集區設定為使用位在相同網站的下一個躍點集區**

1.  開啟 拓撲產生器，以滑鼠右鍵按一下需要變更的 Edge 集區，再按一下 \[編輯內容\] 。

2.  按 \[下一個躍點\] 。從 \[下一個躍點集區:\] 清單中，選取現在要作為下一個躍點集區的集區。

3.  按一下 \[確定\] ，然後發行變更。

**將 Edge 集區設定為使用位在不同網站的下一個躍點集區**

1.  開啟 Lync Server 管理命令介面視窗，並輸入下列 Cmdlet：
    
        Set-CsEdgeServer -Identity EdgeServer:<Edge Server pool FQDN> -Registrar Registrar:<NextHopPoolFQDN>

**在發生災害時容錯移轉集區**

1.  在 Pool2 中的前端伺服器上輸入下列 Cmdlet，找出哪個集區是 中央管理伺服器的主機：
    
        Invoke-CsManagementServerFailover -Whatif
    
    此 Cmdlet 的結果會顯示哪個集區目前裝載了 中央管理伺服器。在此程序的其餘部分，這個集區稱為 CMS\_Pool。

2.  使用拓撲產生器來尋找在 CMS\_Pool 上執行的 Lync Server 版本。如果是執行 Lync Server 2013，請使用下列 Cmdlet 來尋找 Pool1 的備份集區。
    
        Get-CsPoolBackupRelationship -PoolFQDN <CMS_Pool FQDN>
    
    讓 Backup\_Pool 成為備份集區。

3.  使用下列 Cmdlet 來檢查 中央管理存放區的狀態：
    
        Get-CsManagementStoreReplicationStatus -CentralManagementStoreStatus 
    
    此 Cmdlet 應該會顯示 ActiveMasterFQDN 和 ActiveFileTransferAgents 都指向 CMS\_Pool 的 FQDN。如果是空的，則 中央管理伺服器無法使用，您必須將它容錯移轉。

4.  如果 中央管理存放區無法使用，或者 中央管理存放區是在 Pool1 (也就是失敗的集區) 上執行，您必須先容錯移轉 中央管理伺服器，再容錯移轉集區。如果您需要容錯移轉裝載在執行 Lync Server 2013 之集區上的 中央管理伺服器，請使用此程序步驟 5 中的 Cmdlet。如果您需要容錯移轉裝載在執行 Lync Server 2010 之集區上的 中央管理伺服器，請使用此程序步驟 6 中的 Cmdlet。如果您不需要容錯移轉 中央管理伺服器，則跳到此程序的步驟 7。

5.  若要容錯移轉執行 Lync Server 2013 之集區上的 中央管理存放區，請執行下列動作：
    
      - 首先，輸入下列命令，檢查 Backup\_Pool 中的哪個後端伺服器執行 中央管理存放區的主體執行個體：
        
            Get-CsDatabaseMirrorState -DatabaseType Centralmgmt -PoolFqdn <Backup_Pool Fqdn>
    
      - 如果 Backup\_Pool 中的主要後端伺服器是主體，請輸入：
        
            Invoke-CSManagementServerFailover -BackupSQLServerFqdn <Backup_Pool Primary BackEnd Server FQDN> -BackupSQLInstanceName <Backup_Pool Primary SQL Instance Name>
        
        如果 Backup\_Pool 中的鏡像後端伺服器是主體，請輸入：
        
            Invoke-CSManagementServerFailover -MirrorSQLServerFqdn <Backup_Pool Mirror BackEnd Server FQDN> -MirrorSQLInstanceName <Backup_Pool Mirror SQL Instance Name>
    
      - 驗證 中央管理伺服器容錯移轉完成。輸入下列命令：
        
            Get-CsManagementStoreReplicationStatus -CentralManagementStoreStatus 
        
        檢查 ActiveMasterFQDN 和 ActiveFileTransferAgents 指向 Backup\_Pool 的 FQDN。
    
      - 最後，輸入下列命令，檢查所有 前端伺服器的複本狀態：
        
            Get-CsManagementStoreReplicationStatus 
        
        檢查所有複本的值為 True。
        
        跳到此程序的步驟 7。

6.  在 Backup\_Pool 的後端伺服器上安裝 中央管理存放區。
    
      - 首先，執行下列命令：
        
        ``` 
        Install-CsDatabase -CentralManagementDatabase -Clean -SqlServerFqdn <Backup_Pool Back End Server FQDN> -SqlInstanceName rtc  
        ```
    
      - 在 Backup\_Pool 的其中一個前端伺服器上執行下一個命令，以強制移動 中央管理存放區：
        
            Move-CsManagementServer -ConfigurationFileName c:\CsConfigurationFile.zip -LisConfigurationFileName c:\CsLisConfigurationFile.zip -Force 
    
      - 驗證移動完成：
        
            Get-CsManagementStoreReplicationStatus -CentralManagementStoreStatus 
        
        檢查 ActiveMasterFQDN 和 ActiveFileTransferAgents 指向 Backup\_Pool 的 FQDN。
    
      - 輸入下列命令，檢查所有前端伺服器的複本狀態：
        
            Get-CsManagementStoreReplicationStatus 
        
        檢查所有複本的值為 True。
    
      - 在 Backup\_Pool 中的其餘前端伺服器上安裝 中央管理伺服器服務。若要執行這項作業，請在所有前端伺服器 (在此程序稍早用來強制 中央管理存放區移動的伺服器除外) 上執行下列命令：
        
            Bootstrapper /Setup 

7.  在 Lync Server 管理命令介面視窗中執行下列 Cmdlet，將使用者從 Pool1 容錯移轉至 Pool2：
    
        Invoke-CsPoolFailover -PoolFQDN <Pool1 FQDN> -DisasterMode -Verbose
    
    由於在此程序前幾個部分中，用來檢查 中央管理存放區狀態的步驟並非一體適用，所有這個 Cmdlet 還是有可能會因為 中央管理存放區未完全容錯移轉而失敗。在此情況下，您必須根據所看到的錯誤訊息來修正 中央管理存放區，然後重新執行這個 Cmdlet。
    
    如果您看到下列錯誤訊息，則需要先變更位在此網站的 Edge 集區，以使用不同集區作為其下一個躍點，再容錯移轉集區。如需詳細資訊，請參閱本主題一開始的程序。
    
        Invoke-CsPoolFailOver : This Front-end pool "pool1.contoso.com" is specified in
        topology as the next hop for the Edge server. Failing over this pool may cause External
        access/Federation/Split-domain/XMPP features to stop working. Please use Topology Builder to
        change the Edge internal next hop setting to point to a different Front-end pool,  before you
        proceed.

