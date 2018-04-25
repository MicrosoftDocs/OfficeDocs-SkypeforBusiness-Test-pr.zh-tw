---
title: 利用綜合交易測試常設聊天室伺服器
TOCTitle: 利用綜合交易測試常設聊天室伺服器
ms:assetid: 414e43f3-0074-4ecf-a232-398de972cb24
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204837(v=OCS.15)
ms:contentKeyID: 49290718
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 利用綜合交易測試常設聊天室伺服器

 

_**上次修改主題的時間：** 2012-09-21_

針對兩名使用者在聊天室互相傳送與接收訊息進行 常設聊天室伺服器 測試

    Test-CsPersistentChatMessage [-Authentication <TrustedServer | Negotiate | ClientCertificate | 
        LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] -TargetFqdn <String> [-Force <SwitchParameter>] [-OutLoggerVariable <String>] 
        [-OutVerboseVariable <String>] [<CommonParameters>]

或

    Test-CsPersistentChatMessage [-Authentication <TrustedServer | Negotiate | ClientCertificate | 
        LiveID>] -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> [-RegistrarPort 
        <Int32>] -SenderCredential <PSCredential> -SenderSipAddress <String> [-TargetFqdn <String>] [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [<CommonParameters>]

或

    Test-CsPersistentChatMessage [-Authentication <TrustedServer | Negotiate | ClientCertificate | 
        LiveID>] [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable 
        <String>] [<CommonParameters>]

