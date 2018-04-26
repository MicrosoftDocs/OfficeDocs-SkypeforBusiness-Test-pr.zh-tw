---
title: Lync Server 2013：增強及保護資料庫
TOCTitle: 增強及保護 Lync Server 2013 的資料庫
ms:assetid: 6953e721-3511-4235-b848-51bab093dc89
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn518330(v=OCS.15)
ms:contentKeyID: 60471183
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 增強及保護 Lync Server 2013 的資料庫

 

_**上次修改主題的時間：** 2013-12-05_

Microsoft Lync Server 2013 也會將使用者資訊、會議狀態、封存資料及詳細通話記錄 (CDR) 儲存在 SQL Server 資料庫中。您可以分割應用程式資料，來提高容錯性與簡化疑難排解作業，以最大化 Lync Server 2013 後端資料庫上之 Lync Server 資料的可用性。若要達成這些目標，您可以下列方式分割應用程式資料：

  - **使用伺服器分割最佳做法**   使作業系統、應用程式及程式檔案獨立於資料檔案。

  - **儲存交易記錄檔與資料庫檔案**   將這些檔案分開儲存到加密磁碟或磁碟區，以提高容錯性及復原能力。

  - **使用伺服器叢集**   將後端伺服器組成叢集，以最佳化 Lync Server 2013 系統的可用性。

  - **確定所有資料備份皆已加密及正確處理**   無論是備份媒體遺失、遭到刪除或誤植，皆可能會對 Lync Server 2013 部署的資料安全性造成重大的威脅

在 Standard Edition 伺服器以外的所有 Lync Server 2013 伺服器上，皆無法從遠端存取 SQL Server Express 執行個體 (RTCLOCAL 執行個體)，同時除了 Standard Edition 伺服器上的 SQL Server Express 之外，也不會建立任何本機防火牆例外。在 Standard Edition 伺服器上，後端資料庫及中央管理存放區 (CMS) 皆會設定成可從遠端存取。若要強化 SQL Server 資料庫，可以執行下列作業：

  - 自訂 Standard Edition 伺服器上的 SQL Server Express 防火牆，限制可從遠端存取資料庫之伺服器的範圍。預設所有的 IP 位址皆可從遠端存取資料庫。

  - 使用 SQL Server 組態管理員指定通訊協定、IP 位址及 SQL Server 遠端存取的連接埠：
    
      - Lync Server 2013 使用 TCP/IP 通訊協定。其支援 IP 版本 4 (IPv4)，但不支援 IP 版本 6 (IPv6)。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Lync Server 2013 可以在啟用雙重 IP 堆疊的網路中運作。</td>
        </tr>
        </tbody>
        </table>
    
      - Lync Server 2013 支援多個 IP 位址 (多重主目錄網路位址卡)。您可以指定 SQL Server 僅接聽特定的 IP 位址 (個別位址或按照子網路)，以及只使用特定的通訊協定。
    
      - Lync Server 2013 支援靜態和動態 SQL Server 連接埠。

  - 只在靜態 (非預設) 連接埠上執行 SQL Server，而不執行 SQL Server 瀏覽器 (使之無法將接聽連接埠回報給用戶端)。這需要每部 SQL Server 用戶端上自訂設定，包括前端伺服器、監控伺服器、封存伺服器及管理主控台 (執行 Lync Server 管理命令介面、Lync Server 控制台或拓撲產生器)，以及所有執行 Lync Server 資料庫的其他伺服器)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>必須限制只有信任的資料庫管理員才可存取資料庫。惡意的資料庫管理員可能會藉由將資料插入資料庫或加以修改而獲取 Lync Server 2013 伺服器的權限，或是從服務獲取機密的資訊，即使資料庫管理員並未取得 Lync Server 2013 伺服器的直接存取或控制亦是如此。</td>
</tr>
</tbody>
</table>


如需自訂設定及強化 SQL Server 資料庫的詳細資訊，請參閱 NextHop 部落格文章＜搭配使用 Lync Server 2010 與自訂的 SQL Server 網路設定 ＞(英文)，網址是：[http://go.microsoft.com/fwlink/p/?LinkId=214008](http://go.microsoft.com/fwlink/p/?linkid=214008) 。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以強化作業系統及應用程式伺服器，以及使用群組原則在 Lync Server 部署中實作安全性鎖定。如需詳細資訊，請參閱<a href="lync-server-2013-hardening-and-protecting-servers-and-applications.md">增強及保護 Lync Server 2013 的伺服器和應用程式</a>。</td>
</tr>
</tbody>
</table>

