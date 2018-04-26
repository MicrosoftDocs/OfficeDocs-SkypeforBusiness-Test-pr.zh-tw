---
title: Lync Server 2013：刪除聊天室或類別
TOCTitle: 刪除聊天室或類別
ms:assetid: adccb869-0015-4eba-ac73-718bac7843b5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ215881(v=OCS.15)
ms:contentKeyID: 49291987
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中刪除聊天室或類別

 

_**上次修改主題的時間：** 2012-11-01_

可刪除 常設聊天室。如果您不再使用某個聊天室，可以將它停用。如需詳細資訊，請參閱 [在 Lync Server 2013 中停用或啟用聊天室](lync-server-2013-disabling-or-enabling-a-chat-room.md)。

常設聊天室系統管理員可查詢停用的聊天室，然後使用 Windows PowerShell Cmdlet **Remove-CsPersistentChatRoom** 定期清除與永久刪除該聊天室。

可刪除類別。不過，若要刪除類別，您必須先刪除該類別下的所有聊天室或將聊天室移至新類別，保留空白的類別來進行刪除。 常設聊天室伺服器 不允許您刪除包含聊天室的類別。如需詳細資訊，請參閱 [在 Lync Server 2013 中將聊天室從某個類別移到另一個類別](lync-server-2013-moving-a-chat-room-from-one-category-to-another.md)。

如需關於使用 Windows PowerShell 命令列介面刪除空白類別的詳細資訊，請參閱 [使用 Windows PowerShell Cmdlet 設定常設聊天室伺服器](configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md) 中的「聊天室管理」。

如需關於聊天室與類別的詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中設定聊天室](lync-server-2013-configure-rooms.md)與 [在 Lync Server 2013 中設定類別](lync-server-2013-configure-categories.md)。

