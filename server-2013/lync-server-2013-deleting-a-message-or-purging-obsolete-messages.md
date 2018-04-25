---
title: Lync Server 2013：刪除訊息或清除過時的訊息
TOCTitle: 刪除訊息或清除過時的訊息
ms:assetid: 3f0c612d-6dfd-41a4-a5fe-5ff3448eb0ce
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ215874(v=OCS.15)
ms:contentKeyID: 49290694
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中刪除訊息或清除過時的訊息

 

_**上次修改主題的時間：** 2014-02-05_

常設聊天室管理員可以從 常設聊天室的聊天室中刪除訊息 (還可以選擇以其他訊息取代)。管理員也可以清除過時訊息作為持續維護的一部分，以將資料庫的成長最小化。例如，此 Windows PowerShell 命令可從使用者 kenmyer@litwareinc.com 所張貼的 ITChatRoom 聊天室中移除所有訊息：

    Remove-CsPersistentChatMessage -Identity "atl-persistentchat-001.litwareinc.com\ITChatRoom" -UserUri "sip:kenmyer@litwareinc.com"

且此範例會取代任何移除的訊息，並提供訊息不再可以使用的附註：

    Remove-CsPersistentChatMessage -Identity "atl-persistentchat-001.litwareinc.com\ITChatRoom" -UserUri "sip:kenmyer@litwareinc.com" -ReplaceMessage "This message is no longer available."

如需詳細資訊，請參閱 [Remove-CsPersistentChatMessage](remove-cspersistentchatmessage.md) Cmdlet 的說明主題。

