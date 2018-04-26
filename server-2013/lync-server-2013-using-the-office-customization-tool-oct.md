---
title: 使用 Office 自訂工具 (OCT)
TOCTitle: 使用 Office 自訂工具 (OCT)
ms:assetid: 26647cb6-ba84-4ba7-8b6f-2cf86818e530
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204748(v=OCS.15)
ms:contentKeyID: 49290376
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用 Office 自訂工具 (OCT)

 

_**上次修改主題的時間：** 2012-10-02_

Office 自訂工具 (OCT) 屬於安裝程式的一部分，也是許多自訂的建議使用工具。您可以使用 OCT 自訂 Office，並將自訂儲存在安裝程式自訂 .msp 檔案中。您將此檔案放在網路安裝點上的 Updates 資料夾中。當您安裝 Office 時，安裝程式會在 Updates 資料夾中尋找安裝程式自訂檔案，並套用自訂。您僅能在 Office 2013 安裝期間，部署軟體更新時，才能使用 Updates 資料夾。

OCT 屬於安裝程式的一部分，且包含在大量授權版本的產品中。您從包含 Office 2013 來源檔案之網路安裝點的根目錄，藉由在命令列中輸入 `setup.exe /admin` 來執行 OCT，例如使用下列項目：

`\\server\share\Office15\setup.exe /admin`

管理員使用 OCT 建立安裝程式自訂 .msp 檔案。如同在 Microsoft Office 2010 OCT 中一樣，管理員也可以自訂下列區域：

  - **安裝程式** 用於指定在用戶端上的預設安裝位置，以及預設組織名稱、其他網路安裝來源、產品金鑰、使用者授權合約、顯示層級、要移除的 Office 舊版本、安裝期間要執行的自訂程式、安全性設定，以及安裝程式內容。

  - **功能** 用於設定使用者設定，並自訂如何安裝 Office 功能。管理員可以使用 OCT 為使用者指定 Office 應用程式設定的初始預設值。使用者可以在安裝之後修改大多數的設定。

  - **其他內容** 用於新增或移除檔案、新增或移除登錄項目，以及設定捷徑。

  - **Outlook** 用於自訂使用者的預設 Outlook 設定檔、指定 Exchange 設定、新增帳戶、移除帳戶與匯出設定，以及指定傳送/接收群組。

如需 OCT 的資訊，請參閱[http://go.microsoft.com/fwlink/?linkid=267516\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=267516%26clcid=0x404)。

