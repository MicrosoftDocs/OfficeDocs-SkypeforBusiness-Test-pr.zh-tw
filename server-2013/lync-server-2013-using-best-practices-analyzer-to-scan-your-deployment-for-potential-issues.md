---
title: 使用最佳做法分析程式來掃描您的部署可能發生的問題
TOCTitle: 使用最佳做法分析程式來掃描您的部署可能發生的問題
ms:assetid: 09c84509-dc91-4e7b-882b-3c467b6b026d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg591343(v=OCS.15)
ms:contentKeyID: 49290030
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用最佳做法分析程式來掃描您的部署可能發生的問題

 

_**上次修改主題的時間：** 2012-10-21_

若要執行 Best Practices Analyzer 掃描，您必須指定下列各項：

  - **憑證**   若要執行掃描，您必須使用具有本機系統管理員群組成員身分的帳戶，登入已安裝 Best Practices Analyzer 的電腦。此外，當您執行 Best Practices Analyzer 時，用來登入的使用者帳戶需要有執行適當掃描所需的使用者權限，否則，您必須指定具有適當使用者權限的憑證。如需詳細資訊，請參閱＜[最佳做法分析程式的群組成員資格及使用者權限需求](lync-server-2013-group-memberships-and-user-rights-requirements-for-best-practices-analyzer.md)＞。

  - **掃描範圍**   若要指定掃描範圍，請選取您要掃描的類別和伺服器。您可以選取所有類別、一或多個類別，或 Lync Server 環境中特定類別的一或多部伺服器。

  - **掃描類型**   狀況檢查掃描是目前唯一可用的掃描類型 (依預設選取)。狀況檢查掃描會產生報告，其中包含範圍中指定之所有伺服器的錯誤、警告和其他資訊。

  - **網路速度**   網路速度選項包括快速 LAN (100 Mbps 或以上)、LAN (10 Mbps)、快速 WAN (1.5 Mbps) 或 WAN (64 kbps)。完成掃描的估計時間取決於此設定。此設定也會用來設定逾時期限。在掃描期間，Best Practices Analyzer 會在指定的時間內等待伺服器回應。如果在指定的逾時期限內未收到回應，就會移到掃描中的下一部伺服器。在比較慢的網路上，這個指定的逾時期限會比較長，以處理較長的網路延遲。建議您為此參數選取拓撲中最慢的連結，這樣該工具才不會太快逾時。

## 掃描 Lync Server 2013 部署

1.  使用具有本機系統管理員群組成員身分以及其他必要使用者權限的帳戶，登入已安裝 Best Practices Analyzer 的電腦。

2.  按一下 \[開始\]，指向 \[所有程式\]，按一下 \[Microsoft Lync Server 2013\]，然後按一下 \[Best Practices Analyzer\]。

3.  在 \[歡迎\] 畫面上，按一下 \[選取相關選項以進行新的掃描\]。

4.  在「連線到 Active Directory」頁面上，確認 **Active Directory 伺服器** 中指定的名稱，然後執行下列其中一項：
    
      - 若要使用您用來登入電腦的憑證執行掃描，請按一下 \[連線到 Active Directory 伺服器\]。
    
      - 若要指定用於 Active Directory 網域服務、Edge Server 或 Exchange Server 的不同憑證，請按一下 \[顯示進階登入選項\]，選取需要個別憑證的每個核取方塊，為所選取的每個核取方塊指定憑證，然後按一下 \[連線到 Active Directory 伺服器\]。
    
    > [!NOTE]  
    > 在開始掃描之前，Best Practices Analyzer 會執行網路及權限檢查，以確保所指定的帳戶憑證有效，而且 Best Practices Analyzer 可以連線到 Active Directory 網域服務。如果該工具是在工作群組伺服器上執行，也會確認它可以連線到周邊網路中的 Edge Server (如果 Edge Server 包含在掃描中)。
    


5.  在「啟動新的最佳作法掃描」頁面上，選取您要包含在掃描中的選項，指定網路速度，然後按一下 \[開始掃描\]。

6.  在「已完成掃描」頁面上，按一下 \[檢視此最佳作法掃描的報告\]。

7.  在「檢視最佳作法報告」頁面上，執行下列其中一項：
    
      - 若要在依伺服器元件排列的清單中檢視報告，請按一下 \[清單報告\]，然後按一下 \[所有議題\] 索引標籤或 \[參考項目\] 索引標籤。
    
      - 若要在依結果類型排列的階層式清單中檢視報告，請按一下 \[樹狀報告\]，然後按一下 \[詳細檢視\] 索引標籤或 \[摘要檢視\] 索引標籤。
    
      - 若要檢視其他報告，請按一下 \[其他報告\]。
    
    > [!NOTE]  
    > 如需 Best Practices Analyzer 報告及其識別之問題的詳細資訊，請參閱＜<a href="lync-server-2013-viewing-and-working-with-reports-created-by-best-practices-analyzer.md">檢視和使用最佳做法分析程式建立的報表</a>＞及＜<a href="lync-server-2013-analyzing-and-resolving-issues-identified-by-best-practices-analyzer.md">分析和解決由最佳做法分析程式所識別的問題</a>＞。
    

