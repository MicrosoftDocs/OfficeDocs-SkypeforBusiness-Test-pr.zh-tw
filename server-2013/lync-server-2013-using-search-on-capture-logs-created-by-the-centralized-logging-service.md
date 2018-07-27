---
title: 在集中式記錄服務建立的擷取記錄上使用搜尋
TOCTitle: 在集中式記錄服務建立的擷取記錄上使用搜尋
ms:assetid: 1b75b218-d84f-47a7-8a0a-b7e016b1cc79
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687982(v=OCS.15)
ms:contentKeyID: 49889962
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在集中式記錄服務建立的擷取記錄上使用搜尋

 

_**上次修改主題的時間：** 2013-02-21_

基於下列原因，集中記錄服務中的搜尋功能是非常實用和強大的：

  - 搜尋和結果是依據您所定義的準則，在單一電腦、集區、網站或全域範圍上所執行的。

  - 您的搜尋可能一開始很廣泛，之後可以縮小至更具鎖定性的準則，如時間、元件或電腦。當搜尋準則變更時，擁有相同記錄的搜尋並不需要再次執行記錄工作階段。

  - 系統會在範圍內的所有電腦和集區中收集搜尋的結果，並將其收集彙總為單一的輸出檔，由該輸出檔來代表搜尋準則的所有結果 (僅限已執行案例，且由案例擷取的資料)。您是使用類似 **Snooper** 或**記事本**之類的工具來讀取輸出檔，以及整個部署的追蹤訊息。

每部個別電腦上的 CLSAgent 會依據案例 (任何給定時間每部電腦可以執行兩個案例) 來建立記錄。CLSAgent 會管理記錄和其相關聯的索引和快取檔案。當您定義並執行搜尋時，搜尋命令會指示 CLSAgent 所應擷取的資訊。CLSAgent 會依據記錄檔、快取檔案和索引檔案來執行查詢，並將搜尋結果傳至 CLSContoller。CLSController 會收到來自搜尋範圍內所有電腦和集區的搜尋結果。之後，CLSController 會彙總 (組合) 記錄，並以時間差順序排列，最舊的項目優先，依序進行，最新的項目則最後處理。

每次搜尋之後，系統會執行 **Sync-CsClsLogging** Cmdlet，並刷新搜尋所用的快取 (使其不與 CLSAgent 所維護的快取檔案產生混淆)。刷新快取可協助確保在 CLSController 進行下一個搜尋作業時，能有全新的記錄和追蹤檔案擷取緩衝區。

若要取得集中記錄服務的完整優勢，您必須充分了解如何設定搜尋以僅傳回和您所搜尋問題相關之電腦和集區記錄的追蹤訊息。

若要使用 Lync Server 管理命令介面來執行集中記錄服務搜尋功能，您必須是 CsAdministrator 或 CsServerAdministrator 角色型存取控制 (RBAC) 安全性群組的成員，或是包含這兩個群組之一的自訂 RBAC 角色。若要傳回已指派此 Cmdlet 的所有 RBAC 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請從 Lync Server 管理命令介面或 Windows PowerShell 提示中，執行下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Lync Server 2013 cmdlet"}

例如：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsClsConfiguration"}

本主題的重點是在說明如何定義搜尋，以最佳化您的疑難排解。

## 若要使用集中記錄服務來執行基本搜尋

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  請確認您的部署有在全域範圍中執行 AlwaysOn 案例，然後在命令提示字元處輸入下列項目：
    
        Search-CsClsLogging -OutputFilePath <string value of path and file to write the output file>
    
    > [!NOTE]  
    > 根據預設，Search-CsClsLogging 會將搜尋結果傳送至主控台，若您想將搜尋結果儲存至檔案，請使用 –OutputFilePath <em>&lt;字串完整檔案路徑&gt;</em>。若要定義 –OutputFilePath 參數，請在參數中包含以字串格式提供的路徑和檔案名稱，並將其用引號括住 (例如 C:\LogFiles\SearchOutput.txt)。在此範例中，您必須確保目錄 C:\LogFiles 確實存在，且您具備資料夾的讀取和寫入 (NTFS 權限為修改) 檔案權限。輸出會持續附加，而不會被覆寫。若您需要個別的檔案，請為每個搜尋定義不同的檔案名稱。
    
    
    例如：
    
        Search-CsClsLogging -OutputFilePath "C:\LogFiles\logfile.txt"

## 若要使用集中記錄服務，在集區或電腦上執行基本搜尋

1.  若要將搜尋限制在特定集區或電腦上，請搭配使用 –Computers 參數和電腦完整名稱所定義的電腦，將其用引號括住，並以逗號區隔，如下所示：
    
        Search-CsClsLogging -Computers <string value of computer names> -OutputFilePath <string value of path and file to write the output file>
    
    例如：
    
        Search-CsClsLogging -Computers "fe01.contoso.net" -OutputFilePath "C:\LogFiles\logfile.txt"

2.  若要搜尋一部以上的電腦，請輸入多個電腦名稱，將其用引號括住，並以逗號分隔，如下所示：
    
        Search-CsClsLogging -Computers "fe01.contoso.net", "fe02.contoso.net", "fe03.contoso.net" -OutputFilePath "C:\LogFiles\logfile.txt"

3.  若您需要搜尋整個集區，而不是單一電腦，請將 –Computers 參數變更為 –Pools，移除電腦名稱，並將其取代為集區，用引號括住，並用逗號區隔。
    
    例如：
    
        Search-CsClsLogging -Pools "pool01.contoso.net" -OutputFilePath "C:\Logfiles\logfile.txt"

4.  使用搜尋命令時，集區可以是部署中的任何集區，例如：前端集區、Edge 集區、Persistent Chat Server 集區或您部署中所定義的其他集區。
    
    例如：
    
        Search-CsClsLogging -Pools "pool01.contoso.net", "pchatpool01.contoso.net", "intedgepool01.contoso.net" -OutputFilePath "C:\Logfiles\logfile.txt"

## 若要使用時間參數來執行搜尋

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  根據預設，搜尋的時間參數的開始時間為您啟動搜尋的前 30 分鐘。也就是說，若您是在 4:00:00 PM 啟動搜尋，搜尋就會搜尋您在 3:30:00 PM 到 4:00:00 PM 之間定義的電腦和集區的記錄。若您需要搜尋目前時間的 60 分鐘或 3 小時以前，請使用 –StartTime 參數並將日期和時間字串設為您希望搜尋啟動的時間。
    
    例如，使用 –StartTime 和 –EndTime 以定義時間和日期範圍時，您可定義於 11/20/2012 的 8 AM 和 9 AM 之間在集區上進行搜尋。您可將輸出路徑設為將結果寫入名稱為 c:\\logfile.txt 的檔案，如下所示：
    
        Search-CsClsLogging -Pools "pool01.contoso.net" -StartTime "11/20/2012 08:00:00 AM" -EndTime "11/20/2012 09:00:00 AM" -OutputFilePath "C:\Logfiles\logfile.txt"
    
    > [!NOTE]  
    > 您所指定的時間和日期字串可以為「日期時間」或「時間日期」。此命令會剖析字串，並使用適當的日期和時間值。
    


3.  若您想擷取 2012 年 11 月 20 日上午 11 點開始的記錄，請定義 –StartTime。除非您指定特定的 –EndTime，否則搜尋的預設時間範圍皆為 30 分鐘。如此一來，搜尋會傳回所定義的電腦或集區在 11:00:00 AM 至 11:30:00 AM 間的記錄。
    
    例如：
    
        Search-CsClsLogging -Pools "pool01.contoso.net" -StartTime "11/20/2012 11:00:00 AM" -OutputFilePath "C:\Logfiles\logfile.txt"

4.  若要在特定一段時間內搜尋記錄，請定義 –StartTime 和 –EndTime。假設您需要電腦 edge01.contoso.net 上 1 PM 至 2:45 PM 的記錄，
    
    例如：
    
        Search-CsClsLogging -Computers "edge01.contoso.net" -StartTime "11/20/2012 1:00:00 PM" -EndTime "11/20/2012 2:45:00 PM" -OutputFilePath "C:\Logfiles\logfile.txt"

## 若要使用其他準則和比對選項執行進階搜尋

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  若要執行命令以收集特定元件的追蹤，請輸入下列項目：
    
        Search-CsClsLogging -Components <components to search on> -OutputFilePath <fully qualified path to output logs>
    
    例如：
    
        Search-CsClsLogging -Components "SIPStack","S4","UserServices" -OutputFilePath "C:\Logfiles\logfile.txt"
    
    如此一來，搜尋會傳回您部署中所有電腦和集區上前 30 分鐘裡包含 SIPStack、S4 和 UserServices 追蹤元件的所有記錄項目。

3.  若要將相同元件的搜尋限制在名稱為 pool01.contoso.net 的前端集區，請輸入：
    
        Search-CsClsLogging -Components "SIPStack","S4","UserServices" -OutputFilePath "C:\Logfiles\logfile.txt"

4.  若命令包含多個參數，其預設搜尋邏輯則會使用邏輯 OR 和所定義的每個參數。您可使用 **–MatchAll** 參數來變更這項行為。若要這麼做，請輸入下列項目：
    
        Search-CsClsLogging -CallId "d0af828e49fa4dcb99f5f80223a634bc" -Components "SIPStack","S4","UserServices" -MatchAll -OutputFilePath "C:\Logfiles\logfile.txt"

5.  若您的案例是設為持續性執行 (例如 AlwaysOn)，或是您已定義長時間執行案例，則記錄可以從本機電腦轉移至檔案共用。您可使用 CacheFileNetworkFolder 參數定義檔案共用，並使用 New-CsClsConfiguration 來建立新的設定，或使用 Set-CsClsConfiguration 修改現有的設定。若您不希望搜尋包括要搜尋之記錄集合中的檔案共用，請使用 SkipNetworkLogs 參數，如下所示：
    
        Search-CsClsLogging -Components "SIPStack","S4","UserServices" -StartTime "11/1/2012 00:00:01 AM" -EndTime "11/20/2012 2:45:00 PM" -SkipNetworkLogs -OutputFilePath "C:\Logfiles\logfile.txt"

