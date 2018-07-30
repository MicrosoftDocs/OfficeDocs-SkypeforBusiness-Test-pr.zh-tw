---
title: Lync Server 2013：設定聊天室
TOCTitle: 設定聊天室
ms:assetid: 8956bd2c-c863-4704-bc65-5c0d83556258
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205067(v=OCS.15)
ms:contentKeyID: 49291583
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定聊天室

 

_**上次修改主題的時間：** 2012-10-06_

設定 常設聊天室一般是由使用者或其他團隊團隊使用 Windows PowerShell 命令列介面進行處理；系統管理員一般不會管理聊天室。不過，如果您必須建立和管理聊天室，可以使用 Windows PowerShell 命令列介面，也可以將自己加入聊天室成為一員並使用 Lync 2013 用戶端。

如需關於使用 Windows PowerShell 命令列介面設定聊天室的詳細資訊，請參閱＜ [使用 Windows PowerShell Cmdlet 設定常設聊天室伺服器](configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md)＞中的「聊天室管理」。

## 管理聊天室中的資料

常設聊天室伺服器 可讓使用者將訊息張貼到 常設聊天室進行共同作業。資料將保留在伺服器上，而且聊天室的成員可以存取包括歷史資料在內資料。不過，不同角色的使用者對於保留的資料擁有不同的存取權，如下列清單所示。

  - 系統管理員可刪除任何聊天室中較早的內容 (例如，特定日期前張貼的內容)，讓資料庫不致累積過多資料。另外，系統管理員可以移除或替換對於特定聊天室而言被視為不適當的訊息。

  - 一般使用者 (包括訊息作者) 無法刪除任何聊天室中的內容。

  - 聊天室管理員可停用聊天室，但是無法刪除聊天室。只有系統管理員才能刪除已經建立的聊天室。

刪除訊息時，您無法復原刪除的動作。不過，如果有備份的話，就能夠還原所刪除的訊息。如果啟用 常設聊天室規範伺服器，舊訊息將保留在規範伺服器中。

> [!NOTE]  
> 這個聊天室資料使用將套用於 Lync Server 2013 和 常設聊天室伺服器 API 應用程式，但是系統管理員角色涉入處理的情況除外。 常設聊天室伺服器 API 無法用來進行任何的系統管理員操作。您必須在 Lync Server 管理命令介面中執行這些操作。


