---
title: Lync Server 2013：將聊天室從某個類別移到另一個類別
TOCTitle: 將聊天室從某個類別移到另一個類別
ms:assetid: 7e93b8f6-5a18-4476-a432-3918e01bcfa6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ215877(v=OCS.15)
ms:contentKeyID: 49291462
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中將聊天室從某個類別移到另一個類別

 

_**上次修改主題的時間：** 2012-11-01_

建議您不要在建立聊天室後變更 常設聊天室的類別。不過，如果聊天室管理員擁有其他類別的「建立者」 權限，即可將一個類別中的聊天室移到另一個類別。未刪除或重新建立聊天室。這是與資料庫的關聯出現變更。

變更聊天室類別的機會應該很少。類別會決定允許的聊天室成員資格，因此，將聊天室移到另一個類別時，將清除新類別不再支援的所有系統存取控制清單 (SACL)。例如，如果使用者原先是聊天室的成員，但不再是新類別中的 **AllowedMember**，將修改聊天室成員資格，並且從聊天室移除該使用者。

如需使用 Windows PowerShell 命令列介面移動聊天室的詳細資訊，請參閱＜ [使用 Windows PowerShell Cmdlet 設定常設聊天室伺服器](configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md)＞中的「聊天室管理」。

如需設定聊天室的詳細資訊，請參閱部署文件中的＜ [在 Lync Server 2013 中設定聊天室](lync-server-2013-configure-rooms.md)＞。

