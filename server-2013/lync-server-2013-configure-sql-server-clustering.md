---
title: 在 Lync Server 2013 中設定 SQL Server 叢集
TOCTitle: 在 Lync Server 2013 中設定 SQL Server 叢集
ms:assetid: d7b52ef1-573c-48ed-bb94-34e37b49645c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn383982(v=OCS.15)
ms:contentKeyID: 56559317
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定 SQL Server 叢集

 

_**上次修改主題的時間：** 2014-01-10_

Microsoft Lync Server 2013 支援 SQL Server 2012 與 SQL Server 2008 R2 的叢集功能。如需相關支援的詳細資訊，請參閱＜[Lync Server 2013 中的資料庫軟體支援](lync-server-2013-database-software-support.md)＞。

您應先安裝並設定 SQL Server 叢集，然後再安裝並部署 Enterprise Edition 前端伺服器與後端資料庫。如需 SQL Server 2012 容錯移轉叢集的最佳做法與安裝說明，請參閱：<http://technet.microsoft.com/zh-tw/library/hh231721.aspx>。若是 SQL Server 2008 容錯移轉叢集，請參閱 <http://technet.microsoft.com/zh-tw/library/ms189134(v=sql.105).aspx>。

在安裝 SQL Server 時，應安裝 SQL Server Management Studio 以管理資料庫與記錄檔的位置。您在安裝 SQL Server 時，可以選用性元件的形式安裝 SQL Server Management Studio。

> [!IMPORTANT]  
> 若要在 SQL Server 伺服器上安裝及部署資料庫，您必須是資料庫檔案安裝所在之 SQL Server 伺服器的 SQL Server sysadmin 群組成員。如果您不是 SQL Server sysadmin 群組的成員，則必須要求將自己新增至該群組，直到資料庫檔案完成部署為止。如果您無法成為 sysadmin 群組的成員，則應將用以設定及部署資料庫的指令碼提供給 SQL Server 資料庫系統管理員。如需完成程序所需之適當使用者權利和權限的詳細資訊，請參閱＜<a href="lync-server-2013-deployment-permissions-for-sql-server.md">Lync Server 2013 中 SQL Server 的部署權限</a>＞。



## 設定 SQL Server 叢集

1.  完成 SQL Server 叢集的安裝與設定後，您可以使用 SQL Server 執行個體虛擬叢集名稱 (如同在安裝程序中為 SQL Server 叢集設定的名稱) 與 SQL Server 資料庫的執行個體名稱，在拓撲產生器中定義 SQL Server 存放區。不同於單一 SQL Server 伺服器，針對叢集 SQL Server 伺服器，您會使用虛擬節點完整網域名稱 (FQDN)。
    
    > [!NOTE]  
    > 您不需為拓撲產生器設定個別的 Windows Server 叢集節點。您將只會使用虛擬 SQL Server 叢集名稱。
    


2.  如果要使用拓撲產生器部署您的資料庫，您必須是 SQL Server sysadmin 群組的成員。如果您是 SQL Server sysadmin 群組的成員，但不具網域中的權限 (例如 SQL Server 資料庫系統管理員角色)，則您在 Lync Server 中將只有建立資料庫的權限，而無讀取必要資訊的權限。如需部署 Lync Server 所需之使用者權利與權限的詳細資訊，請參閱＜[Lync Server 2013 中 SQL Server 的部署權限](lync-server-2013-deployment-permissions-for-sql-server.md)＞。

3.  使用 SQL Server Management Studio，確定資料庫資料夾與記錄檔資料夾的預設值均正確對應至 SQL Server 叢集中的共用磁碟。如果您要使用拓撲產生器建立資料庫，則必須執行此程序。
    
    > [!NOTE]  
    > 如果您未安裝 SQL Server Management Studio，可於此時安裝，方法是重新執行 SQL Server 安裝，然後將管理工具選取為現有 SQL Server 部署的新增功能。
    


4.  使用拓撲產生器或 Windows PowerShell Cmdlet 安裝 SQL Server 伺服器的資料庫。若要使用拓撲產生器，請使用下列程序。若要使用 Windows PowerShell Cmdlet，請參閱＜[在 Lync Server 2013 中使用 Lync Server 管理命令介面安裝資料庫](lync-server-2013-database-installation-using-lync-server-management-shell.md)＞。

## 若要使用拓撲產生器建立資料庫

1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\]，然後按一下 \[Lync Server 拓撲產生器\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>下列程序假設您已在拓撲產生器中定義並設定拓撲。如需有關定義拓撲的詳細資訊，請參閱<a href="lync-server-2013-defining-and-configuring-the-topology.md">在 Lync Server 2013 中定義和設定拓撲</a>。若要使用拓撲產生器來發行拓撲及設定資料庫，您必須以具有正確使用者權限與群組成員資格的使用者身分登入。如需必要權限與群組成員資格的相關詳細資訊，請參閱<a href="lync-server-2013-deployment-permissions-for-sql-server.md">Lync Server 2013 中 SQL Server 的部署權限</a>。</td>
    </tr>
    </tbody>
    </table>


2.  在拓撲產生器中發行拓撲時，在 \[建立資料庫\] 頁面中，按一下 \[進階\]。

3.  \[選取資料庫檔案位置\] 頁面上有兩個選項，可決定資料庫檔案部署至 SQL Server 叢集的方式。請選取下列其中一項：
    
      - \[自動判斷資料庫檔案位置\]：此選項會使用演算法，根據 SQL Server 伺服器上的磁碟機設定來決定資料庫記錄檔與資料檔的位置。檔案將以此方式分配，以期達到最佳效能。
    
      - \[使用 SQL Server 執行個體預設值\]：選取此選項後，將會根據 SQL Server 執行個體的設定安裝記錄檔與資料檔。將資料庫檔案部署至 SQL Server 後，SQL Server 資料庫系統管理員可能會依據您特定的 SQL Server 設定需求，來重新配置檔案位置，以期達到最佳效能。

4.  完成拓撲發行作業，並確認作業期間未發生任何錯誤。

