---
title: Lync Server 2013：建立或編輯新聊天室
TOCTitle: 建立或編輯新聊天室
ms:assetid: aa8f4349-cfd9-4036-9c4d-de8fb2c4c8a4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ215880(v=OCS.15)
ms:contentKeyID: 49291978
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立或編輯新聊天室

 

_**上次修改主題的時間：** 2015-03-19_

常設聊天室的聊天室通常是由使用者設定； 常設聊天室管理員通常不會設定或管理聊天室。只有 **CsPersistentChatAdministrator** 管理員可以使用 Windows PowerShell Cmdlet 來管理聊天室。

在任何指定的類別中擔任「建立者」 的使用者可以使用 Lync 用戶端來建立和管理聊天室。被任命為特定聊天室管理員的使用者，也可以執行聊天室管理工作，例如編輯聊天室內容或成員資格。

> [!TIP]
> 常設聊天室管理員也可以是「建立者」，但不受「建立者」限制之規範。


如果您是 常設聊天室管理員，則可選擇利用使用者介面來建立和管理聊天室，而非使用 Windows PowerShell Cmdlet。若要這麼做，請啟用 常設聊天室伺服器 管理員的 SIP，然後使用 Lync 用戶端來建立和管理聊天室。

如果要建立使用者的自訂聊天室管理工作流程，您可以設定 常設聊天室伺服器 組態的 **RoomManagementUrl** 內容，將使用者從 Lync 用戶端重新導向至您的自訂解決方案。

如需關於使用 Windows PowerShell 命令列介面設定聊天室的詳細資訊，請參閱＜ [使用 Windows PowerShell Cmdlet 設定常設聊天室伺服器](configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md)＞中的「聊天室管理」。

如需設定聊天室的詳細資訊，請參閱部署文件中的＜ [在 Lync Server 2013 中設定聊天室](lync-server-2013-configure-rooms.md)＞。

