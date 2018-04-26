---
title: Lync Server 2013：停用或啟用聊天室
TOCTitle: 停用或啟用聊天室
ms:assetid: db0908fc-aae3-46e8-bc0b-245e9adfa1e2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ215883(v=OCS.15)
ms:contentKeyID: 49292517
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中停用或啟用聊天室

 

_**上次修改主題的時間：** 2014-02-05_

如果 常設聊天室 聊天室的主題不再重要，您可以停用聊天室，讓使用者無法使用它。停用聊天室時，會立即與聊天室中的所有成員中斷連線。聊天室停用之後，使用者無法再次加入該聊天室，聊天室搜尋中也找不到該聊天室。

已停用的聊天室仍可於稍後由 常設聊天室 管理員啟用。停用聊天室時，其中的成員資格清單與其他設定仍會保留。因此當您再次啟用聊天室時，就不需要手動重新建立設定。

如果聊天室的記錄持續 (聊天室記錄持續性是類別的選用設定，適用於該類別內的所有聊天室；預設是處於持續，但您可以將類別的 \[啟用聊天記錄\] 設定為 false 來關閉)，則在聊天室停用時，該內容就會予以保留。不過，聊天室處於停用狀態的期間，其內容不會出現在搜尋中。如果您之後啟用了聊天室，使用者即可搜尋在聊天室停用前就已張貼的訊息。

如需使用 Windows PowerShell 命令列介面 來停用和啟用聊天室的詳細資訊，請參閱 [使用 Windows PowerShell Cmdlet 設定常設聊天室伺服器](configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md)中的＜聊天室管理＞。若要停用聊天室，請使用類似下列的命令：

    Set-CsPersistentChatRoom -Identity "atl-cs-001.litwareinc.com\ITChatRoom" -Disabled $True

若要啟用聊天室，請將停用屬性設定為 False：

    Set-CsPersistentChatRoom -Identity "atl-cs-001.litwareinc.com\ITChatRoom" -Disabled $False

請注意，不可使用 Lync Server 控制台 啟用或停用聊天室。

如需設定聊天室的詳細資訊，請參閱部署文件中的＜ [在 Lync Server 2013 中設定聊天室](lync-server-2013-configure-rooms.md)＞。

