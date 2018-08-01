---
title: Lync Server 2013：容錯回復常設聊天室伺服器
TOCTitle: 容錯回復常設聊天室伺服器
ms:assetid: 67b91de4-6ddc-43e6-9812-5e1aa84a7980
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204970(v=OCS.15)
ms:contentKeyID: 49291171
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中容錯回復常設聊天室伺服器

 

_**上次修改主題的時間：** 2014-02-05_

此程序概要說明從 常設聊天室伺服器 失效中復原，及從主要資料中心重新建立作業所需的步驟。

在 常設聊天室伺服器 失效期間，主要資料中心會完全中斷，而且主要和鏡像資料庫也無法使用。主要資料中心會容錯移轉至備份伺服器。

在備份主要資料中心，及重建伺服器後，下列程序會還原正常作業。程序假設主要資料中心已經從完全中斷中復原，且已使用 拓撲產生器重建並重新安裝 MGC 資料庫和 Mgccomp 資料庫。

程序也假設在容錯移轉期間未部署新的鏡像和備份伺服器，且唯一所部署的伺服器為備份伺服器及其鏡像伺服器，如同在 [在 Lync Server 2013 中容錯移轉常設聊天室伺服器](lync-server-2013-failing-over-persistent-chat-server.md) 中所定義的。

災難導致主要伺服去失敗，作業轉移至備份伺服器，因為災難發生前設定就存在，設計這些步驟就是用來還原設定。

## 後端 常設聊天室伺服器 容錯回復

1.  透過 Lync Server 管理命令介面使用 `Set-CsPersistentChatActiveServer` Cmdlet，從 常設聊天室伺服器 動態伺服器清單清除所有伺服器。這樣會在容錯回復期間讓所有 常設聊天室伺服器 停止連線至 MGC 資料庫和 Mgccomp 資料庫。
    
    > [!IMPORTANT]  
	> 次要 常設聊天室伺服器 後端伺服器上的 SQL Server 代理程式應當在權限帳戶下執行。具體來說，帳戶必須包括：
    > <ul>
    > <li><p>對備份所在位置之網路共用的讀取存取權。</p></li>
    > <li><p>對備份複製目的位置之特定本機目錄的寫入存取權。</p></li>
    > </ul>


2.  停用備份 MGC 資料庫上的鏡像：
    
    1.  使用 SQL Server Management Studio 連線至備份 MGC 執行個體。
    
    2.  用滑鼠右鍵按一下 MGC 資料庫，指向 **\[工作\]** ，然後按一下 **\[鏡像\]** 。
    
    3.  按一下 **\[移除鏡像\]** 。
    
    4.  按一下 \[確定\] 。
    
    5.  使用 Mgccomp 資料庫執行相同步驟。

3.  備份 MGC 資料庫以便將其還原至新的主要資料庫：
    
    1.  使用 SQL Server Management Studio 連線至備份 MGC 執行個體。
    
    2.  用滑鼠右鍵按一下 MGC 資料庫，指向 **\[工作\]** ，然後按一下 **\[備份\]** 。 **\[備份資料庫\]** 對話方塊隨即顯示。
    
    3.  在 **\[備份類型\]** 中選取 **\[完整\]** 。
    
    4.  針對 **\[備份元件\]** 按一下 **\[資料庫\]** 。
    
    5.  接受 **\[名稱\]** 中建議的預設備份組名稱，或為備份組輸入不同名稱。
    
    6.  *\<選用\>* 在 **\[描述\]** 中輸入備份組的描述。
    
    7.  從目的地清單移除預設備份位置。
    
    8.  使用您為記錄傳送建立的共用位置路徑來將檔案新增至清單。主要資料庫和備份資料庫均可使用此路徑。
    
    9.  按一下 **\[確定\]** 以關閉對話方塊並開始備份程序。

4.  使用先前步驟中建立的備份資料庫來還原主要資料庫。
    
    1.  使用 SQL Server Management Studio 以連線至主要 MGC 執行個體。
    
    2.  以滑鼠右鍵按一下 MGC 資料庫，依序指向 **\[工作\]** 和 **\[還原\]** ，然後按一下 **\[資料庫\]** 。 **\[還原資料庫\]** 對話方塊隨即顯示。
    
    3.  選取 **\[來源裝置\]** 。
    
    4.  按一下開啟 **\[指定備份\]** 對話方塊的 \[瀏覽\] 按鈕。在 **\[備份媒體\]** 中，選取 **\[檔案\]** 。按一下 **\[新增\]** ，選取您在步驟 3 中建立的備份檔案，然後按一下 **\[確定\]** 。
    
    5.  在 **\[選取要還原的備份組\]** 中選取備份。
    
    6.  在 **\[選取頁面\]** 窗格中按一下 **\[選項\]** 。
    
    7.  在 **\[還原選項\]** 中選取 **\[覆寫現有資料庫\]** 。
    
    8.  在 **\[復原狀態\]** 中選取 **\[讓資料庫保持備妥可用\]** 。
    
    9.  按一下 **\[確定\]** 開始復原程序。

5.  針對主要資料庫設定 SQL Server 記錄傳送。遵循 [在 Lync Server 2013 中針對高可用性和災害復原設定常設聊天室伺服器](lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md) 中的程序，針對主要 MGC 資料庫建立記錄傳送。

6.  設定 常設聊天室伺服器 作用中的伺服器。在 Lync Server 管理命令介面使用 **Set-CsPersistentChatActiveServer** Cmdlet 來設定作用中伺服器的清單。
    
    > [!IMPORTANT]  
    > 所有作用中的伺服器必須位於與新主要資料庫相同的資料中心，或位於具有低延遲/高頻寬資料庫連線的資料中心內。
    


若樣將集區還原至其正常狀態，請執行下列 Windows PowerShell 命令：

    Set-CsPersistentChatState -Identity "service: lyncpc.dci.discovery.com" -PoolState Normal

如需詳細資訊，請參閱 [Set-CsPersistentChatState](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsPersistentChatState) Cmdlet 的說明主題。

