---
title: Lync Server 2013：在伺服器上安裝作業系統和必要軟體
TOCTitle: 在伺服器上安裝作業系統和必要軟體
ms:assetid: 055991e0-5aeb-43fc-a7ba-d4b02316d73b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398103(v=OCS.15)
ms:contentKeyID: 49289954
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在伺服器上安裝 Lync Server 2013 的作業系統和必要軟體

 

_**上次修改主題的時間：** 2014-07-24_

在您設定硬體和系統基礎結構之後，除了在您所部署的每一部伺服器上安裝所有先決條件軟體以外，您還需要安裝適當的 Windows 作業系統和更新。這包括每一個 Lync Server 2013 伺服器角色，以及部署所需的任何額外的基礎結構伺服器或執行 SQL Server 的伺服器。

> [!NOTE]  
> 本節說明作業系統的安裝以及內部伺服器的先決條件軟體。如果您正在部署 Edge Server 以支援外部使用者存取，您也需要安裝這些伺服器 (包含 Edge Server 和反向 Proxy 伺服器) 的作業系統和先決條件軟體。如需準備伺服器以支援外部使用者存取的詳細資訊，請參閱部署文件中的＜<a href="lync-server-2013-preparing-for-installation-of-servers-in-the-perimeter-network.md">在周邊網路中準備安裝 Lync Server 2013 的伺服器</a>＞。



## 在伺服器上安裝 Windows 作業系統

依照下列方式，在您所部署的每部伺服器上，安裝適當的 Windows 作業系統：

  - **執行 Lync Server 2013 的伺服器**   如需執行 Lync Server 2013 的伺服器之作業系統需求的詳細資訊，請參閱支援文件中的＜[Lync Server 2013 中的伺服器及工具作業系統支援](lync-server-2013-server-and-tools-operating-system-support.md)＞。

  - **資料庫伺服器**   如需資料庫伺服器 (包括後端資料庫、 封存資料庫及 監控資料庫) 之作業系統需求的詳細資訊，請參閱 SQL Server 文件。若為 SQL Server 2012，請參閱 SQL Server 2012 線上叢書，網址為 [http://go.microsoft.com/fwlink/?linkid=218015\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=218015%26clcid=0x404)。

> [!NOTE]
> 若要在 Windows Server 2008 R2 SP1 上安裝 Lync Server 2013，您必須先安裝 Microsoft 知識庫文章 2646886＜FIX：當模組呼叫 IIS 7.5 的 InsertEntityBody 方法時，發生堆積損毀＞(網址為 <a href="http://go.microsoft.com/fwlink/?linkid=3052%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=3052&amp;clcid=0x404</a>) 中所述的更新。<br />
> 您還必須以知識庫文章中所述方式修改登錄，<a href="http://go.microsoft.com/fwlink/p/?linkid=506893">事件識別碼 32402 和 61045 會記錄在 Windows Server 2012 R2 所安裝的 Lync Server 2013 Front End 伺服器上</a>。


## 在伺服器上安裝 Windows Update

在每部伺服器上安裝 Windows Update 的下列更新：

  - **適用於執行 Lync Server 2013 伺服器的 Windows Update**   如需執行 Lync Server 2013 伺服器所需之 Windows Update 更新的詳細資訊，請參閱規劃文件中的＜[Lync Server 2013 的其他軟體需求](lync-server-2013-additional-software-requirements.md)＞。

  - **資料庫伺服器**   如需資料庫伺服器 (包括後端資料庫、 封存資料庫及 監控資料庫) 所需之 Windows Update 更新的詳細資訊，請參閱 SQL Server 2012 文件。若為 SQL Server 2012，請參閱 SQL Server 2012 線上叢書，網址為 [http://go.microsoft.com/fwlink/?linkid=218015\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=218015%26clcid=0x404)。

## 在伺服器上安裝其他必備軟體

Lync Server 2013 需要在伺服器上安裝下列其他軟體：

  - **執行 Lync Server 2013 伺服器的必要軟體**   執行 Lync Server 2013 伺服器的其他軟體先決條件取決於正在部署的伺服器角色。如需每部伺服器之特定軟體需求的詳細資訊，請參閱規劃文件中的＜[Lync Server 2013 的其他軟體需求](lync-server-2013-additional-software-requirements.md)＞。

  - **Windows Identity Foundation**    Lync Server 2013 需要安裝 Windows Identity Foundation，才能支援伺服器對伺服器驗證案例。若要確認您的電腦上已安裝該軟體，請至 \[控制台\]，依序按一下 \[程式和功能\] 及 \[檢視安裝的更新\] ，然後檢視 \[Microsoft Windows\] 底下。如需安裝 Windows Identity Foundation 的詳細資訊，請參閱 [http://go.microsoft.com/fwlink/?linkid=204657\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=204657%26clcid=0x404)。

  - **Microsoft .NET Framework 4.5**    Lync Server 2013 需要 64 位元版本的 Microsoft .NET Framework 4.5。

  - **資料庫伺服器的先決條件軟體**   如需資料庫伺服器 (包括後端資料庫、 封存資料庫及 監控資料庫) 所需之 Windows Update 的詳細資訊，請參閱 SQL Server 2012 文件，網址為 [http://go.microsoft.com/fwlink/?linkid=218015\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=218015%26clcid=0x404)。
    
    > [!NOTE]  
    > Lync Server 2013 會自動將 Microsoft SQL Server 2012 Express 安裝到每部 Standard Edition 伺服器 以及每部執行 Lync Server 2013 (這是本機設定存放區所在的位置) 的伺服器上。
    


  - **Windows Media Format Runtime**   所有將部署會議的 前端伺服器 和 Standard Edition 伺服器都必須安裝 Windows Media Format Runtime。需要有 Windows Media Format Runtime，才能執行 Windows Media Audio (.wma) 檔案 (通話駐留、宣告和回應群組應用程式需要此檔案來播放宣告和音樂)。
    
    > [!NOTE]  
    > 對於 Windows Server 2012 和 Windows Server 2012 R2，Windows Media Format Runtime 會與 Microsoft Media Foundation 一同安裝。
    
    
    > [!NOTE]  
    > 對於 Windows Server 2008 和 Windows Server 2008 R2，Windows Media Format Runtime 會安裝為 Windows 桌面體驗的一部分。建議您先安裝 Windows 桌面體驗，再安裝 Lync Server 2013。如果 Lync Server 2013 在伺服器上找不到這個軟體，就會提示您安裝，然後您必須重新啟動伺服器來完成安裝。
    

