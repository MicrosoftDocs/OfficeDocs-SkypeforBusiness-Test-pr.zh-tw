---
title: 讀取集中式記錄服務的擷取記錄
TOCTitle: 讀取集中式記錄服務的擷取記錄
ms:assetid: c86ccf61-d86f-4ebd-b8d1-984a1b73005d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721879(v=OCS.15)
ms:contentKeyID: 49890309
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 讀取集中式記錄服務的擷取記錄

 

_**上次修改主題的時間：** 2013-02-22_

您在執行搜尋後發現 集中記錄服務 的實際優點，那就是它讓您有個檔案可用來追蹤某個回報的問題。您有多種方法可以讀取這個檔案。輸出檔是標準文字格式，您可以使用 Notepad.exe 或任何其他可讓您開啟並讀取文字檔的程式加以開啟。對於較大的檔案和較複雜的問題，則可以使用像是 Snooper.exe 的工具，這款工具是專為讀取及剖析 集中記錄服務 所輸出的記錄而設計。Snooper 隨附在需另行下載的 Lync Server 2013 偵錯工具裡。安裝 Lync Server 2013 偵錯工具時，並不會建立捷徑或功能表項目。安裝完 Lync Server 2013 Debug Tools 後，請開啟 Windows 檔案總管、命令列視窗，或 Lync Server 管理命令介面，然後前往 C:\\Program Files\\Microsoft Lync Server 2013\\Debugging Tools 目錄 (預設位置)。按兩下 Snooper.exe；如果您是使用命令列或 Lync Server 管理命令介面，則輸入 Snooper.exe 再按 ENTER 鍵。

> [!IMPORTANT]  
> 本主題的用意不在詳述及討論疑難排解技巧。疑難排解及其相關程序是個複雜的主題。如需關於疑難排解基本知識和疑難排解特定工作負載的詳細資訊，請參閱位於 <a href="http://go.microsoft.com/fwlink/?linkid=211003%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=211003&amp;clcid=0x404</a> 的＜Microsoft Lync Server 2010 資源套件＞。其程序仍適用於 Lync Server 2013。



Lync Server 2013 引進了更新版本的 Snooper，該版本包含一些新功能。下列螢幕擷取畫面顯示來自 Office Communications Server 2007 的 Snooper 版本。

![Office Communications 2007 版 Snooper。](images/JJ721879.129503a8-8edd-4bb0-a68f-c43f9a548b93(OCS.15).jpg "Office Communications 2007 版 Snooper。")

下列螢幕擷取畫面顯示 Lync Server 2013 偵錯工具中包含的新版 Snooper。

![Lync Server 2013 版 Snooper。](images/JJ721879.131495dd-8220-4ae4-af37-0ac5c318fd45(OCS.15).jpg "Lync Server 2013 版 Snooper。")

下列螢幕擷取畫面顯示含有常用功能的工具列。

![Snooper 2013 工具列。](images/JJ721879.989249c5-a33e-4251-b8b4-411019cc12b2(OCS.15).jpg "Snooper 2013 工具列。")

此外，最新一項帶來更高價值的新功能就是流程圖 (通話流程) 圖表檢視。您可以在 \[訊息\] 索引標籤中選取訊息流程，然後按一下 \[通話流程\] 按鈕。您每換一個訊息，通話流程圖表就會根據新的資料而更新。

![Snooper 2013 通話流程圖。](images/JJ721879.bb8be45d-a842-48fe-86f8-380207d70bab(OCS.15).jpg "Snooper 2013 通話流程圖。")

您可以將滑鼠在圖表檢視上到處移動，以取得有關訊息、流程與訊息之內容，以及伺服器元素等詳細資訊。按一下任何通話流程箭頭即可前往 \[訊息\] 檢視中的該則訊息。

![通話流程圖訊息詳細資料。](images/JJ721879.1147d720-38a9-4bda-8361-78f27ecde3d1(OCS.15).jpg "通話流程圖訊息詳細資料。")

## 在 Snooper 中開啟記錄檔

1.  若要使用 Snooper 開啟記錄檔，您需要記錄檔的讀取權。若要使用 Snooper 存取記錄檔，您必須是 CsAdministrator 或 CsServerAdministrator 角色存取控制 (RBAC) 安全性群組的成員，或是包含這其中任一群組的自訂 RBAC 角色的成員。

2.  安裝 Lync Server 偵錯工具 (LyncDebugTools.msi) 後，使用 Windows 檔案總管或從命令列變更目錄到 Snooper.exe 的位置。偵錯工具預設位於 C:\\Program Files\\Microsoft Lync Server 2013\\Debugging Tools。按兩下或執行 Snooper.exe。

3.  開啟 Snooper 後，以滑鼠右鍵按一下 \[檔案\]、按一下 \[開啟舊檔\]、尋找記錄檔、在 \[開啟檔案\] 對話方塊中選取檔案，然後按一下 \[開啟\]。

4.  記錄檔的 \[追蹤\] 訊息會顯示在 \[追蹤\] 索引標籤。按一下 \[訊息\] 索引標籤可檢視所收集到追蹤的訊息內容。

## 顯示通話流程圖

1.  若要使用 Snooper 開啟記錄檔，您需要記錄檔的讀取權。若要使用 Snooper 存取記錄檔，您需要是 CsAdministrator 或 CsServerAdministrator 角色存取控制 (RBAC) 安全性群組的成員，或是包含這其中任一群組的自訂 RBAC 角色的成員。

2.  開啟記錄檔並按一下 \[訊息\] 索引標籤、在訊息檢視中選取交談，或在 \[追蹤\] 索引標籤上選取追蹤元件。

3.  按一下 \[通話流程\]。
    
    > [!NOTE]  
    > 如果您按一下不屬於通話流程一部分的訊息或追蹤，則不會出現圖表，而是在 Snooper 底端出現狀態訊息，指出「此訊息不具有通話流程的資格」。請選擇另一個訊息或追蹤，如果該訊息或追蹤是通話流程的一部分，便會出現通話流程。
    


4.  在訊息或追蹤行之間移動，並注意通話流程圖表是否有所更新或變成顯示新的圖表。

5.  將滑鼠移到各元素上以取得關於通話訊息、端點及其他元件的資訊。

