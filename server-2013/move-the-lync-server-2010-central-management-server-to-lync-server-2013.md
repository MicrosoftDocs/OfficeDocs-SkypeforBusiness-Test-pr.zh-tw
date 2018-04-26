---
title: 將 Lync Server 2010 中央管理伺服器移至 Lync Server 2013
TOCTitle: 將 Lync Server 2010 中央管理伺服器移至 Lync Server 2013
ms:assetid: 30cc98f2-1916-4dbe-99d0-8df5368ed3ec
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688013(v=OCS.15)
ms:contentKeyID: 49890003
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將 Lync Server 2010 中央管理伺服器移至 Lync Server 2013

 

_**上次修改主題的時間：** 2013-11-25_

從 Lync Server 2010 移轉至 Lync Server 2013 之後，您必須將 Lync Server 2010中央管理伺服器移至 Lync Server 2013前端伺服器或集區，才能移除舊版 Lync Server 2010 伺服器。

中央管理伺服器是一個單一主要/多個複本系統，其中資料庫的讀取/寫入複本是存放在包含 中央管理伺服器的 前端伺服器。拓撲中的每部電腦 (包括包含 中央管理伺服器的 前端伺服器)，在安裝和部署期間，電腦上安裝的 SQL Server 資料庫 (預設名稱為 RTCLOCAL) 中都會具備 中央管理存放區資料的唯讀複本。本機資料庫會透過在所有電腦上以服務方式執行的 Lync Server 複本複寫器代理程式，來接收複本更新。 中央管理伺服器上的實際資料庫和本機複本的名稱是 XDS，其主要是由 xds.mdf 和 xds.ldf 檔案所構成。主要資料庫的位置則由 Active Directory 網域服務中的服務控制點 (SCP) 所參照。所有利用 中央管理伺服器來管理與設定 Lync Server 的工具都會使用 SCP 來找出 中央管理存放區。

成功移動 中央管理伺服器之後，您應從原始 前端伺服器移除 中央管理伺服器資料庫。如需移除 中央管理伺服器資料庫的資訊，請參閱＜ [移除前端集區的 SQL Server 資料庫](remove-the-sql-server-database-for-a-front-end-pool.md)＞。

您可使用 Lync Server 管理命令介面中的 Windows PowerShell Cmdlet **Move-CsManagementServer**，將 Lync Server 2010 SQL Server 資料庫中的資料庫移動至 Lync Server 2013 SQL Server 資料庫，然後再更新 SCP 以指向新的 Lync Server 2013中央管理伺服器位置。

## 準備 Lync Server 2013前端伺服器後再移動 中央管理伺服器

請先使用本節的程序來準備 Lync Server 2013前端伺服器，然後再移動 Lync Server 2010中央管理伺服器。

## 準備 Enterprise Edition 前端集區

1.  在 Lync Server 2013 Enterprise Edition 前端集區上，您想要重新放置 中央管理伺服器：以 **RTCUniversalServerAdmins** 群組成員的身分登入已安裝 Lync Server 管理命令介面的電腦。您也必須具有您要安裝 中央管理存放區所在之資料庫的 SQL Server 資料庫系統管理員使用者權限。

2.  開啟 Lync Server 管理命令介面。

3.  若要在 Lync Server 2013 SQL Server 資料庫中建立新 中央管理存放區，請在 Lync Server 管理命令介面中輸入：
    
        Install-CsDatabase -CentralManagementDatabase -SQLServerFQDN <FQDN of your SQL Server> -SQLInstanceName <name of instance>

4.  確認 **Lync Server 前端** 服務的狀態為 \[已啟動\] 。

## 準備 Standard Edition 前端伺服器

1.  在 Lync Server 2013 Standard Edition 前端伺服器上，您想要重新放置 中央管理伺服器：以 **RTCUniversalServerAdmins** 群組成員的身分登入已安裝 Lync Server 管理命令介面的電腦。

2.  開啟 Lync Server 部署精靈。

3.  在 \[ Lync Server 部署精靈\] 中，按一下 \[準備第一個 Standard Edition Server\] 。

4.  在 \[執行命令\] 頁面上， SQL Server Express已安裝為 中央管理伺服器。已建立所需的防火牆規則。在完成資料庫和必要軟體的安裝時，請按一下 \[完成\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果命令輸出摘要畫面沒有可見的更新，則初始安裝可能需要一些時間。這是由於安裝 SQL Server Express 的緣故。如果您需要監控資料庫的安裝，請使用 [工作管理員] 來監控安裝程式。</td>
    </tr>
    </tbody>
    </table>


5.  若要在 Lync Server 2013 Standard Edition 前端伺服器中建立新 中央管理存放區，請在 Lync Server 管理命令介面中輸入：
    
        Install-CsDatabase -CentralManagementDatabase -SQLServerFQDN <FQDN of your Standard Edition Server> -SQLInstanceName <name of instance - RTC by default>

6.  確認 **Lync Server 前端** 服務的狀態為 \[已啟動\] 。

## 移動 Lync Server 2010中央管理伺服器至 Lync Server 2013

1.  在要當作 中央管理伺服器的 Lync Server 2013 伺服器上：以 **RTCUniversalServerAdmins** 群組成員的身分登入已安裝 Lync Server 管理命令介面的電腦。您也必須具有 SQL Server 資料庫管理員使用者權限。

2.  開啟 Lync Server 管理命令介面。

3.  在 Lync Server 管理命令介面中輸入：
    
        Enable-CsTopology
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果 <code>Enable-CsTopology</code> 沒有成功，請先阻止命令完成並解決問題之後再繼續。如果 <strong>Enable-CsTopology</strong> 沒有成功，移動就會失敗，且可能會導致您的拓撲處於沒有 中央管理存放區的狀態。</td>
    </tr>
    </tbody>
    </table>


4.  在 Lync Server 2013前端伺服器或 前端集區上，於 Lync Server 管理命令介面中輸入：
    
        Move-CsManagementServer

5.  Lync Server 管理命令介面會顯示伺服器、檔案存放區、資料庫存放區以及目前和建議狀態的服務連線點。請詳細閱讀資訊，並確認預期的來源與目的地是否無誤。輸入 \[Y\] 繼續或 \[N\] 停止移動。

6.  檢閱並解決由 **Move-CsManagementServer** 命令所產生的任何警告或錯誤。

7.  在 Lync Server 2013 伺服器上，開啟 \[ Lync Server 部署精靈\]。

8.  在 Lync Server 部署精靈中，依序按一下 \[安裝或更新 Lync Server 系統\] 及 \[步驟 2: 設定或移除 Lync Server 元件\] ，再按 \[下一步\] 檢視摘要，然後按一下 \[完成\] 。

9.  在 Lync Server 2010 伺服器上，開啟 \[ Lync Server 部署精靈\]。

10. 在 Lync Server 部署精靈中，依序按一下 \[安裝或更新 Lync Server 系統\] 及 \[步驟 2: 設定或移除 Lync Server 元件\] ，再按 \[下一步\] 檢視摘要，然後按一下 \[完成\] 。

11. 重新啟動 Lync Server 2013 伺服器。這是必要的，因為有群組成員資格變更為存取 中央管理伺服器 資料庫。

12. 若要確認新的 中央管理存放區有進行複寫，請在 Lync Server 管理命令介面中輸入：
    
        Get-CsManagementStoreReplicationStatus
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>複寫可能要花一些時間來更新所有目前的複本。</td>
    </tr>
    </tbody>
    </table>


## 在移動後移除 Lync Server 2010中央管理存放區檔案

1.  在 Lync Server 2010 伺服器上：以 **RTCUniversalServerAdmins** 群組成員的身分登入已安裝 Lync Server 管理命令介面的電腦。您也必須具有 SQL Server 資料庫管理員使用者權限。

2.  開啟 Lync Server 管理命令介面
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請先確認複寫已完成且狀態穩定後，再繼續移除之前的資料庫檔案。如果您在複寫完成前就移除檔案，會中斷複寫程序，並導致剛移動的 中央管理伺服器處於未知狀態。請使用 <strong>Get-CsManagementStoreReplicationStatus</strong> Cmdlet 來確認複寫狀態。</td>
    </tr>
    </tbody>
    </table>


3.  若要移除來自 Lync Server 2010中央管理伺服器的 中央管理存放區資料庫檔案，請輸入：
    
        Uninstall-CsDatabase -CentralManagementDatabase -SqlServerFqdn <FQDN of SQL Server> -SqlInstanceName <Name of source server>
    
    例如：
    
        Uninstall-CsDatabase -CentralManagementDatabase -SqlServerFqdn sql.contoso.net -SqlInstanceName rtc
    
    其中 *\<FQDN of SQL Server\>* 是 Enterprise Edition 部署中的 Lync Server 2010 後端伺服器，或是 Standard Edition Server 的 FQDN。

