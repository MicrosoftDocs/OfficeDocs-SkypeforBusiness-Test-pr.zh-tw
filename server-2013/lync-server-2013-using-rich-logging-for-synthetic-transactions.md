---
title: 使用綜合交易的豐富記錄
TOCTitle: 使用綜合交易的豐富記錄
ms:assetid: 32714a71-9f42-4d5b-a508-e176d8f08bbf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204798(v=OCS.15)
ms:contentKeyID: 49290525
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用綜合交易的豐富記錄

 

_**上次修改主題的時間：** 2012-10-22_

綜合交易 (已於 Microsoft Lync Server 2010 中引進) 為系統管理員提供一種方式來確認使用者可順利完成一般工作，例如，登入系統、交換立即訊息，或打給位於公用交換電話網路 (PSTN) 的電話。這些測試 (已封裝為一組 Lync ServerWindows PowerShell Cmdlet) 可由系統管理員手動產生，或者可透過像是 System Center Operations Manager 的應用程式自動執行。

在 Lync Server 2010 中，綜合交易已經證明在協助系統管理員識別系統問題時非常有用。例如，**Test-CsRegistration** Cmdlet 可以警示系統管理員，部分使用者在使用 Lync Server 進行登錄時發生問題。但是，綜合交易在協助系統管理員判斷為什麼這些使用者會在使用 Lync Server 進行登錄時發生問題並不是很有用。這是因為綜合交易不會提供詳細記錄資訊，以協助系統管理員針對 Lync Server 的問題進行疑難排解。綜合交易的詳細資訊輸出充其量只能提供逐步資訊，讓系統管理員能夠根據經驗來猜測可能發生問題的地方。

在 Microsoft Lync Server 2013 中，綜合交易已重新建構來提供豐富的記錄。「豐富的記錄」表示將針對綜合交易所進行的每個活動記錄如下的資訊：

  - 活動開始時間

  - 活動完成時間

  - 執行的動作 (例如，建立、加入或離開會議；登入 Lync Server；傳送立即訊息等)

  - 活動執行時所產生的資訊、詳細資料、警告或錯誤訊息

  - SIP 登錄訊息

  - 活動執行時所產生的例外狀況記錄或診斷碼

  - 執行活動的最終結果

此資訊會在每次執行綜合交易時自動產生。但是，資訊不會自動顯示或儲存至記錄檔，而是手動執行綜合交易的系統管理員可使用 OutLoggerVariable 參數來指定 Windows PowerShell 變數，以便將資訊儲存於其中。接著，系統管理員可以在此使用兩個方法，讓他們能夠使用 XML 或 HTML 格式來儲存和/或檢視豐富的記錄。

例如，Lync Server 2010 系統管理員可以使用類似下列的命令來執行 **Test-CsRegistration** Cmdlet：

    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com

系統管理員可以選擇在他們選擇的變數名稱之後包含 OutLoggerVariable 參數：

    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com -OutLoggerVariable RegistrationTest

> [!NOTE]  
> 請不要在變數名稱的開頭加上 $ 字元。請使用像是 RegistrationTest 的變數名稱，而不要使用 $RegistrationTest。



上述命令輸出內容如下：

    Target Fqdn   : atl-cs-001.litwareinc.com
    Result        : Failure
    Latency       : 00:00:00
    Error Message : This machine does not have any assigned certificates.
    Diagnosis     :

不過，系統會顯示更多關於此次失敗的詳細資訊，而不只是上述顯示的錯誤訊息。若要使用 HTML 格式存取該資訊，請使用類似下列的命令，以便將儲存於變數 RegistrationTest 中的資訊儲存至 HTML 檔案：

    $RegistrationTest.ToHTML() | Out-File C:\Logs\Registration.html

或者，您可以使用 ToXML() 方法，將資料儲存至 XML 檔案：

    $RegistrationTest.ToXML() | Out-File C:\Logs\Registration.xml

接著可以使用 Internet Explorer、Visual Studio 或任何其他能夠開啟 HTML/XML 檔案的應用程式來檢視這些檔案。

從 System Center Operations Manager 內部執行的綜合交易將會針對失敗自動產生這些記錄檔。但是，如果在 Windows PowerShell 能夠載入並執行綜合交易之前執行失敗，則將不會產生這些記錄。

> [!IMPORTANT]  
> 根據預設，Lync Server 2013 會將記錄檔儲存於未共用的資料夾。若要使這些記錄隨時都能存取，您應該共用這個資料夾 (例如，\\atl-watcher-001.litwareinc.com\WatcherNode)。


