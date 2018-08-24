---
title: Lync Server 2013：將常設聊天室伺服器新增至拓撲
TOCTitle: 將常設聊天室伺服器新增至拓撲
ms:assetid: 8389b307-8c17-4e45-b3b5-5dc9fcfc2ffb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205049(v=OCS.15)
ms:contentKeyID: 49291517
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中將常設聊天室伺服器新增至拓撲

 

_**上次修改主題的時間：** 2012-10-06_

您必須先在拓撲中加入 常設聊天室伺服器 支援的 Lync Server 2013，才能設定您的部署來支援 常設聊天室伺服器。本主題的資訊將描述如何使用 拓撲產生器在現有拓撲中加入 常設聊天室伺服器 支援。

## 在拓撲中加入 常設聊天室伺服器

執行下列步驟，安裝單一 Persistent Chat Server 集區，而不設定災害復原組態。如需設定延伸的 Persistent Chat Server 集區達到高可用性及災害復原的效果，請參閱部署文件中的＜ [在 Lync Server 2013 中針對高可用性和災害復原設定常設聊天室伺服器](lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md)＞。

若要部署多個 Persistent Chat Server 集區，請對於各個集區重複相同的程序。

1.  在執行 Lync Server 2013 的電腦上，或安裝 Lync Server 系統管理工具的電腦上，使用本機 Users 群組成員的帳戶 (或具有相等使用者權限的帳戶) 登入。
    
    > [!NOTE]  
    > 您可以使用本機 Users 群組成員的帳戶來定義拓撲，但是若要發佈拓撲 (需要此動作才能安裝 Lync Server 2013 伺服器)，您必須使用 <strong>Domain Admins</strong> 群組成員及 <strong>RTCUniversalServerAdmins</strong> 群組成員的帳戶，以及在您要用於 常設聊天室伺服器 檔案存放區 (以便 拓撲產生器可設定所需的 DACL) 的檔案存放區上具有完整控制權限 (亦即，讀取、寫入和修改) 的帳戶，或是具有相等權限的帳戶。 UNRESOLVED_TOKEN_VAL()UNRESOLVED_TOKEN_VAL()
    


2.  啟動 拓撲產生器.

3.  在主控台樹狀目錄中，導覽至 \[ 常設聊天室 集區\] 節點，並將節點展開，選取一個 Persistent Chat Server 集區，或者以滑鼠右鍵按一下節點，並選取 \[新增 常設聊天室節點\] 。您必須定義集區的完整網域名稱 (FQDN)，並指出集區將是單一伺服器集區或多重伺服器集區部署。
    
    您可以選擇 \[多重電腦集區\] 或 \[單一電腦集區\] 。如果您打算在 Persistent Chat Server 集區中使用一個以上的 常設聊天室伺服器前端伺服器。立即或稍後選擇，這是因為建立單一電腦集區後，稍後便無法新增其他伺服器。如果您選擇一個以上電腦集區，請輸入組成集區的個別 常設聊天室伺服器前端伺服器所用的名稱。
    
    > [!IMPORTANT]  
    > 如果在 Lync Server 2013Standard Edition 伺服器上安裝 常設聊天室伺服器 角色，FQDN 必須與 Standard Edition 伺服器的 FQDN 相符。
    


4.  定義 Persistent Chat Server 集區的簡單 \[顯示名稱\] 。自訂用戶端可使用顯示名稱，尤其是有多個 Persistent Chat Server 集區區別聊天室。

5.  定義 常設聊天室伺服器用來與 Lync Server前端伺服器進行通訊的連接埠。預設的連接埠為 5041。

6.  如果您的組織需要規範支援，請選取 \[用規範記錄\] 核取方塊。如果選擇，將在同一部電腦上安裝 常設聊天室伺服器 規範服務做為 常設聊天室伺服器前端伺服器。這將稍後提示您選取 SQL Server後端伺服器 用於 常設聊天室伺服器 規範。

7.  指派 Persistent Chat Server 集區的網站相關性。選取 \[使用此集區作為網站 \<網站名稱\> 的預設值\] 核取方塊或 \[使用此集區作為全部網站的預設值\] 指定這個 Persistent Chat Server 集區作為目前網站或全部網站的預設集區。 Lync 2013 用戶端用台建立和管理聊天室時，使用者網站相關的預設集區將用於聊天室建立和管理作業，因此，能夠將聊天室建立和管理作業交由該集區進行。只有在部署多個 Persistent Chat Server 集區，並且要使用 常設聊天室伺服器 的聊天室建立和管理功能時，這才適用。
    
    > [!IMPORTANT]  
    > 您可以使用 常設聊天室伺服器 軟體開發套件 (SDK) 自訂聊天室建立和管理功能。<br />
    > 如需關於如何設定 SQL Server 備份資料庫進行災害復原的詳細資訊，請參閱部署文件中的＜ <a href="lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md">在 Lync Server 2013 中針對高可用性和災害復原設定常設聊天室伺服器</a>＞。


8.  進行下列任一個動作，定義 常設聊天室伺服器 Back End 的 \[(儲存聊天室內容) 的SQL 存放區\] ：
    
      - 若要使用現有的 SQL Server 資料庫，請在下拉式清單中，按一下要使用的 SQL Server 資料庫名稱。
    
      - 若要指定新的 SQL Server 資料庫，請按一下 \[新增\] ，並且在 \[定義新的 SQL 存放區\] 中執行下列動作：
    
    <!-- end list -->
    
      - 在 \[SQL Server FQDN\] 中，指定您要建立新 SQL Server 資料庫的 SQL Server 資料庫 FQDN。
    
      - 選取 \[預設執行個體\] 使用預設執行個體，或者，若要指定不同的執行個體，請選取 \[具名執行個體\] ，並指定要使用的執行個體。

9.  如果已啟用規範，請定義 SQL Server 規範資料庫。
    
    > [!IMPORTANT]  
    > 如需關於如何設定 SQL Server 鏡像使 常設聊天室伺服器 資料庫和 常設聊天室伺服器 規範資料庫達到高可用性的詳細資訊，請參閱部署文件中的＜ <a href="lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md">在 Lync Server 2013 中針對高可用性和災害復原設定常設聊天室伺服器</a>＞。
    


10. 定義檔案存放區。檔案存放區是儲存任何上傳至檔案儲存機制的檔案副本所用的資料夾 (例如，儲存張貼於聊天室的檔案附件)。對於多重伺服器 常設聊天室伺服器 拓撲，這必須是「通用命名慣例」(UNC) 路徑，對於單一伺服器 常設聊天室伺服器 拓撲，這可以是本機檔案路徑。
    
    若要使用現有的檔案存放區，請執行下列動作：
    
      - 在 \[檔案伺服器 FQDN\] 中，指定您要建立新檔案存放區的檔案存放區 FQDN。
    
      - 在 \[檔案共用\] 中，指定要使用的檔案存放區。
    
    > [!IMPORTANT]  
    > 您可以先在 拓撲產生器中定義檔案存放區，然後才建立檔案存放區；但是您必須先在您定義的位置中建立檔案存放區，才能發行拓撲。
    


11. 選取要作為此 Persistent Chat Server 集區下一個躍點的 前端伺服器集區。這是 前端伺服器集區，能夠用來將 常設聊天室伺服器 要求路由到這個集區。

12. 若要儲存組態，請按一下 \[完成\] 。 Persistent Chat Server 集區將出現在特定集區設定所完成的 拓撲產生器中。
    
    若要立即發佈更新過的拓撲到 常設聊天室伺服器，請參閱部署文件中的＜ [在 Lync Server 2013 中發行更新後的拓撲](lync-server-2013-publish-the-updated-topology.md)＞。
    
    > [!NOTE]  
    > 開啟 拓撲產生器時，即可繼續進行＜ <a href="lync-server-2013-publish-the-updated-topology.md">在 Lync Server 2013 中發行更新後的拓撲</a>＞中的步驟 3 開始發佈更新過的拓撲。
    

