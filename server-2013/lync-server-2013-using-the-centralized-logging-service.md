---
title: 使用集中式記錄服務
TOCTitle: 使用集中式記錄服務
ms:assetid: 7b05aaef-f0ea-4649-ba8a-02e68b0cdf23
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688101(v=OCS.15)
ms:contentKeyID: 49890126
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用集中式記錄服務

 

_**上次修改主題的時間：** 2012-11-01_

集中記錄服務是 Lync Server 2013 中的新功能。它是舊版 **OCSLogger** 和 **OCSTracer** 工具的增強替代功能。您可以使用集中記錄服務執行下列功能：

  - 開始從單一位置和命令登入一或多個電腦和集區。

  - 停止從單一位置和命令登入一或多個電腦和集區。

  - 搜尋一或多個電腦和集區上的記錄檔，找出單一位置或命令。您可以量身打造搜尋命令，傳回所有電腦上擷取和儲存的整個記錄檔彙總，或傳回會擷取特定資料的已整理結果。

  - 如下設定記錄工作階段：
    
      - 定義**案例**，或使用預設案例。集中記錄服務中的*案例*包含範圍 (全域或網站)、識別案例目的所用的案例名稱，以及一或多個提供者。您可以在任何指定的時間於一部電腦上執行兩個案例。
    
      - 使用現有*提供者*或建立新的提供者。*提供者*定義記錄工作階段所收集的內容、內容的詳細程度、要追蹤哪些元件，以及要套用哪些旗標。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果您熟悉 OCSLogger，<em>提供者</em>一詞是指<strong>元件</strong> (例如，S4、SIPStack)、<strong>記錄類型</strong> (例如，WPP、EventLog 或 IIS logfile)、<strong>記錄層次</strong> (例如，全部、詳細、偵錯) 及<strong>旗標</strong> (例如，TF_COMPONENT、TF_DIAG) 的集合。這些項目是在提供者 (Windows PowerShell 變數) 中定義，並傳遞到 集中記錄服務 命令。</td>
        </tr>
        </tbody>
        </table>
    
      - 設定要從中收集記錄的電腦和集區。
    
      - 從選項**網站** (僅在該網站中的電腦執行記錄擷取) 或**全域** (在部署中所有的電腦上執行記錄擷取) 定義記錄工作階段的範圍。

集中記錄服務極為強大，幾乎能夠符合大小問題疑難排解的所有需求。從根本原因分析到效能問題，集中記錄服務都是任何系統管理員的重要工具。顯示的所有範例均使用 Lync Server 管理命令介面。名稱為 **CLSController.exe** 的 集中記錄服務 有一個命令列元件。命令列工具本身提供說明。不過，不過，您只能從命令列執行有限的功能。使用 Lync Server 管理命令介面之後，即可存取更多的且更能夠設定的功能集。使用集中記錄服務時，您應該永遠考慮將 Lync Server 管理命令介面作為優先使用的方法。

本小節的主題說明如何使用集中記錄服務，並提供如何使用其中眾多功能的範例。

## 本章節內容

  - [集中式記錄服務概觀](lync-server-2013-overview-of-the-centralized-logging-service.md)

  - [使用 PowerShell 管理集中式記錄服務組態設定](lync-server-2013-managing-the-centralized-logging-service-configuration-settings.md)

  - [瞭解集中式記錄服務組態設定](lync-server-2013-understanding-centralized-logging-service-configuration-settings.md)

  - [將 Start 用於集中式記錄服務以擷取記錄](lync-server-2013-using-start-for-the-centralized-logging-service-to-capture-logs.md)

  - [將 Stop 用於集中式記錄服務](lync-server-2013-using-stop-for-the-centralized-logging-service.md)

  - [在集中式記錄服務建立的擷取記錄上使用搜尋](lync-server-2013-using-search-on-capture-logs-created-by-the-centralized-logging-service.md)

  - [讀取集中式記錄服務的擷取記錄](lync-server-2013-reading-capture-logs-from-the-centralized-logging-service.md)

