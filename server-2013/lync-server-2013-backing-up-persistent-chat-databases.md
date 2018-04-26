---
title: 備份常設聊天室資料庫
TOCTitle: 備份常設聊天室資料庫
ms:assetid: b99ebdc0-a025-44d7-9d74-37a7365f330d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945646(v=OCS.15)
ms:contentKeyID: 52056210
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 備份常設聊天室資料庫

 

_**上次修改主題的時間：** 2013-02-17_

常設聊天室的聊天室內容會儲存在 常設聊天室資料庫 (mgc.mdf) 中。這是重要商業資料，應定期備份。除了聊天室內容，常設聊天室資料庫也會儲存有關主體 (例如使用者和使用者群組) 的資訊，以及角色和他們在聊天室所進行的存取。

備份 常設聊天室 資料有兩種方式。

  - SQL Server 備份

  - `Export-CsPersistentChatData` Cmdlet 可將常設聊天室資料匯出成檔案

使用 SQL Server 備份所建立的資料需要大量的磁碟空間，可能需要比由 `Export-CsPersistentChatData` 所建立的還要多 20 倍空間，但是 SQL Server 備份可能是系統管理員更為熟悉的程序。

