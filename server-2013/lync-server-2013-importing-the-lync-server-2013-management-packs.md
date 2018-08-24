---
title: 匯入 Lync Server 2013 管理組件
TOCTitle: 匯入 Lync Server 2013 管理組件
ms:assetid: 846287e1-660f-453f-bdba-b2137b5f0ea1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205052(v=OCS.15)
ms:contentKeyID: 49291528
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 匯入 Lync Server 2013 管理組件

 

_**上次修改主題的時間：** 2012-10-22_

您可以安裝管理組件 (指示 System Center Operations Manager 可監視哪些項目以及應該如何監視這些項目和如何觸發並回報通知的軟體)，擴充 System Center Operations Manager 的功能。Lync Server 2013 包含兩個 System Center Operations Manager 管理組件，提供下列功能：

  - 元件與使用者管理套件 (Microsoft.LS.2013.Monitoring.ComponentAndUser.mp) 可追蹤的 Lync Server 問題包含事件記錄中所記錄的問題、效能計數器登錄的問題，或詳細通話記錄 (CDR) 或品質經驗 (QoE) 資料庫所記錄的問題。對於重大問題，可設定 System Center Operations Manager 立即透過電子郵件、立即訊息或短訊息服務 (SMS) 訊息通知系統管理員。SMS 是行動裝置之間互傳文字訊息的技術。
    
    > [!NOTE]  
    > 如需關於設定 Operations Manager 通知的詳細資訊，請參閱 TechNet Library 的「設定通知」(<a href="http://go.microsoft.com/fwlink/?linkid=268785%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268785&amp;clcid=0x404</a>)。
    


  - Active Monitoring Management Pack (Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp) 會主動測試重要的 Lync Server 元件，例如登入系統、互傳立即訊息，或者與公用交換電話網路 (PSTN) 上的電話通話。這些測試是使用 Lync Server 綜合交易 Cmdlet 進行。例如，您可以使用 **Test-CsIM** Cmdlet 模擬兩個測試使用者之間的立即訊息 (IM) 交談。如果這個模擬的訊息交談失敗，將產生通知。

您需要匯入管理組件。如果不匯入管理組件，則無法使用 Operations Manager 監視 Lync Server 事件或執行 Lync Server 綜合交易。

Component and User Management Pack 僅用於監視 Lync Server 2013。如果是在同時安裝 Lync Server 2013 和 Lync Server 2010 的共存環境下，您應該對於 Lync Server 2010 電腦繼續使用 Lync Server 2010 管理組件。

> [!NOTE]  
> Lync Server 2010 的管理組件包含 Lync Server 2010 Monitoring Management Pack 及 Lync Server 2010 Group Chat Monitoring Management Pack。



您可以使用下列工具匯入管理組件：

  - **System Center Operations Manager**   藉由這個方法，將使用 Operations Manager 加入 Lync Server 的監視。

  - **Operations Manager Shell**   您可以使用 Operations Manager 命令介面直接匯入，或解決使用 System Center Operations Manager 主控台匯入管理組件時發生的任何問題。

## 使用 System Center Operations Manager 匯入管理組件

1.  下載 Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp 及 Microsoft.LS.2013.Monitoring.ComponentAndUser.mp 兩個檔案。

2.  在 System Center Operations Manager 中，按一下 \[系統管理\] 。

3.  在 \[系統管理\] 中，以滑鼠右鍵按一下 \[管理組件\]，然後按一下 \[匯入管理組件\]。

4.  在 \[選取管理組件\] 對話方塊中，按一下 \[新增\]，然後按一下 \[從磁碟新增\]。

5.  在 \[線上目錄連線\] 對話方塊中，按一下 \[取消\] 可避免 Operations Manager 上線，以查看 Lync Server 管理組件是否存在任何相依性。如果您使用 System Center Operations Manager 2012，請按一下 \[否\]。

6.  在 \[選取要匯入的管理組件\] 對話方塊中，找出並選取 \[Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp\] 及 \[Microsoft.LS.2013.Monitoring.ComponentAndUser.mp\] 兩個檔案，然後按一下 \[開啟\]。若要選取對話方塊中的多個檔案，請按一下第一個檔案，並按住 Ctrl 鍵，然後按一下第二個檔案。

7.  在 \[選取管理組件\] 對話方塊中，按一下 \[安裝\]。如果出現錯誤訊息，而且安裝失敗，這一般是表示管理組件位於 Windows 使用者帳戶控制所保護的資料夾中。如果發生這種情況，請將檔案複製到不同的資料夾，然後重新開始匯入和安裝程序。

8.  在 \[選取管理組件\] 對話方塊中，按一下 \[關閉\]。請注意，匯入和安裝程序可能需要幾分鐘才會完成。

## 使用 Operations Manager 命令介面匯入管理組件

一般而言，使用 Operations Manager 較容易匯入管理組件。不過，如果，如果發生錯誤，導致匯入失敗，主控台將無法確實提供充分的錯誤報告。相較之下，Operations Manager 命令介面可提供詳細的資訊。如果您使用 Operations Manager，但是無法匯入管理組件，請使用 Operations Manager 命令介面匯入組件。Operations Manager 命令介面可提供更多有助於您判斷匯入失敗原因的資訊。

如果您使用 System Center Operations Manager 2007 R2，請完成下列程序：

1.  依序按一下 \[開始\] \> \[所有程式\] \> \[System Center Operations Manager 2007 R2\] \> \[Operations Manager 命令介面\]。

2.  在 Operations Manager 命令介面中，輸入在命令提示字元下使用 Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp 檔案實際路徑輸入下列命令，並按下 ENTER 鍵：
    
        MPImport.exe D:\MP\Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp

3.  匯入第一個管理組件後，使用 Microsoft.LS.2013.Monitoring.ComponentAndUser.mp 檔案的路徑重複進行這個程序：
    
        MPImport.exe D:\MP\Microsoft.LS.2013.Monitoring.ComponentAndUser.mp

4.  關閉 Operations Manager 命令介面。

如果您使用 System Center Operations Manager 2012，則請完成下列程序：

1.  依序按一下 \[開始\] \> \[所有程式\] \> \[Microsoft System Center 2012\] \> \[Operations Manager\] \> \[\[Operations Manager 命令介面\]。

2.  在 Operations Manager 命令介面中，輸入在命令提示字元下使用 Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp 檔案實際路徑輸入下列命令，並按下 ENTER 鍵：
    
        Import-SCOMManagementPack -FullName "D:\MP\ Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp"

3.  匯入第一個管理組件後，使用 Microsoft.LS.2013.Monitoring.ComponentAndUser.mp 檔案的路徑重複進行這個程序：
    
        Import-SCOMManagementPack -FullName "D:\MP\ Microsoft.LS.2013.Monitoring.ComponentAndUser.mp"

