---
title: 集中式記錄服務概觀
TOCTitle: 集中式記錄服務概觀
ms:assetid: 975718a0-f3e3-404d-9453-6224e73bfdd0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688145(v=OCS.15)
ms:contentKeyID: 49890220
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 集中式記錄服務概觀

 

_**上次修改主題的時間：** 2013-02-22_

集中記錄服務旨在提供一種受控制的方式來廣域或狹域地收集資料。您可以同時向位於部署中的所有伺服器收集資料、定義要追蹤的特定元素、設定追蹤旗標，以及傳回來自單一電腦的搜尋結果或是來自所有伺服器的所有資料彙總。集中記錄服務會在位於部署中的所有伺服器上執行。集中記錄服務的架構包含下列代理程式與服務：

  - *集中記錄服務代理程式*   ClsAgent.exe 是服務執行檔，其會與控制器通訊，並且接收管理員對控制器發出的命令。代理程式會在每部 Lync Server 電腦上以服務的形式執行。代理程式在收到命令時，會執行命令、傳送訊息給已定義的元件進行追蹤，然後將追蹤記錄寫入磁碟。它也會讀取其所在電腦的追蹤記錄，並且可應要求將追蹤資料傳送回控制器。ClsAgent 會在下列連接埠上接聽命令：**TCP 50001**、**TCP 50002** 及 **TCP 50003**。

  - *集中記錄服務控制器*   ClsControllerLib.dll 是 Lync Server 管理命令介面與 ClsController.exe 所用的命令執行引擎。CLSControllerLib.dll 會傳送 Start、Stop、Flush 與 Search 命令給 ClsAgent。傳送搜尋命令時，產生的記錄會傳回給 ClsControllerLib.dll 進行彙總。控制器即在負責傳送命令給代理程式、接收這些命令的狀態、在位於搜尋範圍中任何電腦上的所有代理程式傳回了搜尋記錄檔資料時加以管理，並且將記錄資料彙總成有意義和經過排序的輸出集。下列主題中的資訊著重在 Lync Server 管理命令介面的使用。ClsController.exe 只具備 Lync Server 管理命令介面所提供的一小部分特色與功能。如需 ClsController.exe 的說明，可以在命令列中於預設目錄 C:\\Program Files\\Common Files\\Microsoft Lync Server 2013\\ClsAgent 下輸入 `ClsController`。

**ClsController 對 ClsAgent 的通訊**

![CLSController 與 CLSAgent 之間的關係。](images/JJ688145.68c90811-5cf9-4a84-95b7-ea9ffc61eac4(OCS.15).jpg "CLSController 與 CLSAgent 之間的關係。")

您可以使用 Windows Server 命令列介面或 Lync Server 管理命令介面發出命令。命令會在您登入的電腦上執行，並傳送給本機的 ClsAgent 或傳送給位於部署中的其餘電腦與集區。

ClsAgent 會維護一份索引檔案來指出其在本機電腦上的所有 .CACHE 檔案。ClsAgent 會配置這些檔案，讓這些檔案平均分散在 CacheFileLocalFolders 選項所定義的各磁碟區，且確保絕對不會耗用每個磁碟區超過 80% 的空間 (您可以使用 **Set-CsClsConfiguration** Cmdlet 來設定本機快取位置與百分比)。ClsAgent 也負責從本機中清理掉所快取的老舊事件追蹤記錄 (.etl) 檔案。兩週之後 (您可以使用 **Set-CsClsConfiguration** Cmdlet 設定此時間範圍)，這些檔案會複製到檔案共用並自本機電腦中刪除。如需詳細資訊，請參閱 [Set-CsClsConfiguration](set-csclsconfiguration.md)。收到搜尋要求時，系統會使用搜尋條件來選取快取的 .etl 檔案集，以根據代理程式所維護之索引中的值來執行搜尋。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ClsAgent 可以搜尋從本機電腦移至檔案共用的檔案。ClsAgent 將檔案移至檔案共用之後，就不負責維護檔案的老舊清理和移除。您應該定義管理工作來監視檔案共用中檔案的大小並進行刪除或封存。</td>
</tr>
</tbody>
</table>


可用來讀取和分析所產生記錄檔的工具有很多，包括 **Snooper.exe** 和任何可以讀取文字檔的工具 (例如 **Notepad.exe**)。Snooper.exe 是 Lync Server 2013 偵錯工具的一部分，可以從網路下載。

如同 OCSLogger，集中記錄服務有數項元件可以做為追蹤依據，並且提供選取如 TF\_COMPONENT 和 TF\_DIAG 等旗標的選項。集中記錄服務也會保留 OCSLogger 的記錄層級選項。

比起使用命令列 ClsController，使用 Windows PowerShell 最重要的優點是您可以使用選取的提供者，針對問題空間、自訂旗標及記錄層級來設定及定義新的案例。ClsController 僅能使用已針對該執行檔定義的案例。

先前版本提供了 OCSLogger.exe 來讓系統管理員和支援人員向位於部署中的電腦收集追蹤檔案。OCSLogger 儘管功能強大，卻仍有一項缺點：在同一時間內只能收集一部電腦上的記錄。您可以使用多份 OCSLogger 來分別登入多部電腦，但最終會得到多個記錄，而且無法輕易彙總這些結果。

當使用者要求搜尋記錄時，ClsController 會根據選取的案例決定要將要求傳送給哪些機器。它也會決定是否要將搜尋傳送至儲存之 .etl 檔案所在的檔案共用。當搜尋結果傳回給 ClsController 時，控制器會將結果合併成呈現給使用者看的單一排序結果集。使用者可以將搜尋結果儲存至其本機電腦做進一步分析。

當您啟動記錄工作階段時，您會指定與目前所嘗試解決之問題有關的案例。不論何時，您都可以有兩個案例在執行。其中一個案例應該是 AlwaysOn 案例。正如其名，此案例應該一律在您的部署中執行，收集所有電腦、集區與元件上的資訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，AlwaysOn 案例不會在您的部署中執行。您必須明確啟動該案例。啟動之後，它會持續執行 (即使電腦重新開機也一樣) 直到被明確停止為止。如需關於啟動及停止案例的詳細資訊，請參閱＜<a href="lync-server-2013-using-start-for-the-centralized-logging-service-to-capture-logs.md">將 Start 用於集中式記錄服務以擷取記錄</a>＞及＜<a href="lync-server-2013-using-stop-for-the-centralized-logging-service.md">將 Stop 用於集中式記錄服務</a>＞。</td>
</tr>
</tbody>
</table>


當有問題發生時，請開始進行跟所報告問題有關的第二個案例。重現問題，然後讓第二個案例停止記錄。開始進行跟所報告問題有關的記錄搜尋。收集到的記錄會全部彙總成一個記錄檔，其中包含來自您某個網站中或全域部署範圍中之所有電腦的追蹤訊息。如果搜尋傳回的資料超過可行的分析範圍 (通常稱為訊雜比；其中的雜訊過高)，便須以範圍較小的參數執行另一個搜尋。此時，您可以開始在出現的模式中，注意是否有能夠幫助您專注於問題的模式。最後，在執行幾次精化的搜尋之後，您就能夠找到與問題有關的資料，並查出根本原因。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Lync Server 中看到問題案例時，請問問自己：「我對這個問題知道多少？」如果您將問題的範圍量化，就可以省去 Lync Server 中絕大部分的操作。<br />
假設有一個案例是您知道使用者在查詢連絡人時無法取得最新的結果。在媒體元件、企業語音、會議功能及其他數個元件中尋找問題並無意義。您可能並不知道問題的實際發生位置：這是用戶端還是伺服器端的問題？連絡人是由 User Replicator 自 Active Directory 收集而來，並經由 Address Book Server (ABServer) 傳送至用戶端。ABServer 會從 RTC 資料庫取得更新 (這些更新是由 User Replicator 寫入至資料庫)，並在預設時間 (上午 1:30) 將更新收錄到通訊錄檔案中。Lync Server 用戶端會依隨機的排程擷取新的通訊錄。知道整個流程，就能夠縮小可能原因的搜尋範圍，來查出問題是與 User Replicator 從 Active Directory 收集的資料、ABServer 並未擷取及建立通訊錄，還是用戶端未下載通訊錄檔案有關。</td>
</tr>
</tbody>
</table>

