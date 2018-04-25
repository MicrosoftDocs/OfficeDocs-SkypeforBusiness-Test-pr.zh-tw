---
title: Lync Server 2013 檔案儲存支援
TOCTitle: 檔案儲存支援
ms:assetid: ed66430d-3c19-4267-938c-956a51005073
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399073(v=OCS.15)
ms:contentKeyID: 49292719
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的檔案儲存支援

 

_**上次修改主題的時間：** 2012-10-16_

Lync Server 2013 使用同一個檔案存放區來存放所有檔案。檔案存放區支援下列功能：

  - 在 Direct Attached Storage (DAS) 或存放區域網路 (SAN) 上的檔案共用，包括分散式檔案系統 (DFS) 以及在獨立磁碟容錯陣列 (RAID) 上進行檔案儲存。如需儲存需求的詳細資訊，請參閱規劃文件中的 [Lync Server 2013 中的前端伺服器、立即訊息及顯示狀態的技術需求](lync-server-2013-technical-requirements-for-front-end-servers-instant-messaging-and-presence.md) 和 [Lync Server 2013 中 Director 的軟硬體需求](lync-server-2013-hardware-and-software-requirements-for-the-director.md)。如需 Windows Server 2008 作業系統 DFS 的詳細資訊，請參閱＜Windows Server 2008 DFS 逐步指南＞，網址為 [http://go.microsoft.com/fwlink/?LinkId=202835\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=202835%26clcid=0x404)。

  - 檔案共用的共用叢集。如果您使用共用叢集，您應使用執行 Windows Server 2008 或 Windows Server 2008 R2 的叢集伺服器。使用執行舊版 Windows 的叢集伺服器可能因為權限問題導致無法使用某些功能。請使用叢集管理員來建立檔案共用。如需使用叢集管理員的詳細資訊，請參閱 Microsoft 知識庫文件 284838＜如何使用 Cluster.exe 建立伺服器叢集檔案共用＞(機器翻譯)，網址為 [http://go.microsoft.com/fwlink/?linkid=140899\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=140899%26clcid=0x404)。

