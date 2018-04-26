---
title: 安裝 SQL Server Reporting Services
TOCTitle: 安裝 SQL Server Reporting Services
ms:assetid: 638a1d0c-1ac7-4735-83f2-4df3d03c7cf9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204957(v=OCS.15)
ms:contentKeyID: 49291111
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 安裝 SQL Server Reporting Services

 

_**上次修改主題的時間：** 2012-06-20_

若想使用 Microsoft Lync Server 2013 監控報告 (如需詳細資訊，請參閱本文件下一節)，必須先安裝 SQL Server Reporting Services；您可以在安裝 Microsoft SQL Server 的同時或之後的任何時間安裝 Reporting Services。如果尚未安裝 SQL Server，請遵循本文件中先前提供的指示。安裝 SQL Server 時，請務必在 \[特徵選取\] 頁面選取 \[Reporting Services\]。如此會安裝 SQL Server Reporting Services。

若已安裝 SQL Server 但未安裝 SQL Server Reporting Services，您可以視情況遵循針對 SQL Server 2008 R2 或 SQL Server 2012 的一組適當指示，新增該特徵。

若要驗證已成功安裝 Reporting Services，請完成下列步驟：

1.  如果執行 Microsoft SQL Server 2008 R2，請依序按一下 **\[開始\]**、**\[所有程式\]**、**\[Microsoft SQL Server 2008 R2\]**、\[**組態工具\]** 及 **\[Reporting Services 組態管理員\]**。
    
    如果執行 Microsoft SQL Server 2012，請依序按一下 **\[開始\]**、**\[所有程式\]**、**\[Microsoft SQL Server 2012\]**、**\[組態工具\]** 及 **\[Reporting Services 組態管理員\]**。

2.  在 **\[Reporting Services 組態連接\]** 對話方塊中，確認您伺服器的名稱顯示在 **\[伺服器名稱\]** 方塊中，而儲存您監控資料之 SQL Server 執行個體的名稱顯示在 **\[報表伺服器執行個體\]** 方塊中，然後按一下 **\[連接\]**。

在 Reporting Services 組態管理員中，\[報表伺服器狀態\] 窗格應該顯示已安裝 SQL Server Reporting Services，以及正在執行 Reporting Services：報表伺服器狀態應顯示為 **\[已啟動\]**，且 **\[啟動\]** 按鈕應該呈現灰色而無法使用。如果 Reporting Service 未執行，請按一下 **\[啟動\]** 以啟動服務。

如果 \[報表伺服器資料庫名稱\] 標籤旁未列出資料庫，請執行下列作業：

1.  在 Reporting Services 組態管理員中，按一下 **\[資料庫\]**。

2.  在 \[報表伺服器資料庫\] 窗格中，按一下 **\[變更資料庫\]**。

3.  在報表伺服器資料庫組態精靈的 \[動作\] 窗格中，選取 **\[建立新的報表伺服器資料庫\]**，然後按 **\[下一步\]**。

4.  在報表伺服器資料庫組態精靈的 \[資料庫伺服器\] 窗格中，確認列於 **\[伺服器名稱\]**、**\[驗證類型\]** 及 **\[使用者名稱\]** 方塊中的資訊是否正確。按一下 **\[測試連接\]** 以驗證可以連接至資料庫伺服器，然後按 **\[下一步\]**。

5.  在報表伺服器資料庫組態精靈的 \[資料庫\] 窗格中，接受 **\[資料庫名稱\]**、**\[語言\]** 及 **\[報表伺服器模式\]** 的預設值，然後按 **\[下一步\]**。

6.  在報表伺服器資料庫組態精靈的 \[認證\] 窗格中，確認列於 **\[驗證類型\]** 下拉式清單、**\[使用者名稱\]** 及 **\[密碼\]** 方塊中的資訊是否正確，然後按 **\[下一步\]**。

7.  在報表伺服器資料庫組態精靈的 \[摘要\] 窗格中，按 **\[下一步\]**。

8.  在報表伺服器資料庫組態精靈的 \[進度和完成\] 窗格中，按一下 **\[完成\]**。

若要驗證是否設定 Reporting Service URL，請按一下 **\[Web 服務 URL\]**。應該見到在 **\[報表伺服器 Web 服務 URL\]** 標題下列出一個或多個 URL。請逐一按一下這些 URL，確認是否可以存取本機安裝 SQL Server Reporting Services 的首頁。

