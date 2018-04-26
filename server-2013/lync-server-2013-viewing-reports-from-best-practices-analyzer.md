---
title: 檢視最佳做法分析程式的報表
TOCTitle: 檢視最佳做法分析程式的報表
ms:assetid: 7217a47b-36b1-4923-81ea-df754cff29bb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg607690(v=OCS.15)
ms:contentKeyID: 49291291
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視最佳做法分析程式的報表

 

_**上次修改主題的時間：** 2012-09-21_

在使用最佳做法分析程式掃描環境的時候，需指定掃描的名稱。一旦最佳做法分析程式完成掃描，就會將掃描結果儲存在報告中以及掃描名稱下方。掃描完成時，您可直接從 **\[已完成掃描\]** 頁面按一下 **\[檢視此最佳作法掃描的報告\]** 來檢視掃描所產生的報告，亦可稍後再從該掃描或先前的掃描檢視報告。您可於執行掃描的本機電腦上檢視報告、從其他電腦匯入掃描結果或匯出掃描結果以在已安裝最佳做法分析程式的其他電腦上檢視報告。

掃描結果會以下列報告類型顯示：

  - 清單報告

  - 樹狀報告

  - 其他報告

這些報告包括錯誤、警告及其他資訊。如需有關每項報告與問題類型的詳細資訊，請參閱＜[瞭解最佳做法分析程式建立的報表](lync-server-2013-understanding-reports-created-by-best-practices-analyzer.md)＞。

使用下列程序檢視最佳做法分析程式先前產生的掃描結果。

## 從先前的掃描檢視報告

1.  使用本機使用者帳戶之成員的帳戶登入已安裝最佳做法分析程式的電腦。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可使用本機系統管理員群組成員的帳戶檢視掃描結果，但無法執行掃描，除非您具有適當的使用者權利與權限。如需詳細資訊，請參閱＜<a href="lync-server-2013-group-memberships-and-user-rights-requirements-for-best-practices-analyzer.md">最佳做法分析程式的群組成員資格及使用者權限需求</a>＞。</td>
    </tr>
    </tbody>
    </table>


2.  按一下 **\[開始\]**，指向 **\[所有程式\]**，按 **\[Microsoft Lync Server 2013\]**，然後再按 **\[最佳做法分析程式\]**。

3.  在 **\[歡迎\]** 畫面上按一下 **\[選取要檢視的掃描結果\]**。

4.  在 **\[選取要檢視的最佳作法掃描\]** 頁面上，執行下列其中一項作業：
    
      - 若要從本機儲存的掃描結果清單檢視報告，請按一下掃描名稱，然後按 **\[檢視此掃描的報告\]**。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>最佳做法分析程式會從 <em>&lt;systemDrive&gt;</em>\Documents and Settings\<em>&lt;user&gt;</em>\Application Data\Microsoft\RtcBPA 資料夾建立本機檔案清單。</td>
        </tr>
        </tbody>
        </table>
    
      - 若要檢視儲存於其他位置的掃描結果報告，請按一下 **\[匯入掃描\]**，尋找包含有掃描結果的檔案，然後按 **\[開啟\]**。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果電腦上的最佳做法分析程式版本與已匯入檔案中用於收集資料的版本不相符，檔案匯入之後，電腦上的工具可能會再分析一次。</td>
        </tr>
        </tbody>
        </table>


5.  在 **\[檢視最佳作法報告\]** 頁面上，執行下列其中一項作業：
    
      - 若要檢視伺服器元件所組織的報告，請按一下 **\[清單報告\]**，然後按 **\[所有問題\]** 索引標籤或 **\[參考項目\]** 索引標籤。
    
      - 若要檢視由結果類型所組織成的階層式清單，請按一下 **\[樹狀報告\]**，然後按 **\[詳細檢視\]** 索引標籤或 **\[摘要檢視\]** 索引標籤。
    
      - 若要檢視其他報告，請按一下 **\[其他報告\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如需有關最佳做法分析程式報告及其找出問題的詳細資訊，請參閱 <a href="lync-server-2013-viewing-and-working-with-reports-created-by-best-practices-analyzer.md">檢視和使用最佳做法分析程式建立的報表</a> 與 <a href="lync-server-2013-analyzing-and-resolving-issues-identified-by-best-practices-analyzer.md">分析和解決由最佳做法分析程式所識別的問題</a>。</td>
    </tr>
    </tbody>
    </table>

