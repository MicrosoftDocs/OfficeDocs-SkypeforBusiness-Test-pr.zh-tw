---
title: 管理類別
TOCTitle: 管理類別
ms:assetid: 1b118d91-b4c4-4b2f-b842-b451417ec2c6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204719(v=OCS.15)
ms:contentKeyID: 49290252
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 管理類別

 

_**上次修改主題的時間：** 2012-10-06_

建立新 常設聊天室伺服器 類別

    New-CsPersistentChatCategory -Name Foo -PersistentChatPoolFqdn client.contoso1b118d91-b4c4-4b2f-b842-b451417ec2c6.com [other parameters]

> [!IMPORTANT]  
> 僅有在具備一個以上的 Persistent Chat Server 集區時，才需要 PersistentChatPoolFqdn。



若要變更現有的 常設聊天室伺服器 類別

    Set-CsPersistentChatCategory -Identity testCat -AllowedMembers @{Add="sip:user1@contoso.com", "CN=container,DC=contoso,DC=com"}  -DeniedMembers @{Add="sip:user2@contoso.com"}
    Set-CsPersistentChatCategory -Identity testCat -Creators @{Add="sip:user1@contoso.com"}

Windows PowerShell：可同時設定 AllowedMembers、DeniedMembers, 和 Creators。Creators 應為 AllowedMembers 扣除 DeniedMembers 的子集。您也可以在設定成員和建立者同時設定類別的內容。

## 建立、取得、設定或移除類別

若要建立新類別

    New-CsPersistentChatCategory -Name <String> [-PersistentChatPoolFqdn <String>] [-Description <String>] [-EnableInvitations<Switch Parameter>] [-EnableFileUpload <Switch Parameter>] [-RemoveChatHistory <Switch Parameter>] [-MaxContentSize <Integer>]

若要取得類別

    Get-CsPersistentChatCategory -Identity <String>

或

    Get-CsPersistentChatCategory -PersistentChatPoolFqdn <String>

若要設定類別

    Set-CsPersistentChatCategory -Instance <CategoryObject> [-WhatIf] [-Confirm] [<CommonParameters>]

或

    Set-CsPersistentChatCategory [-Identity] <string> [-Name <string>] [-Description <string>] [-Invitations <bool>] [-FileUpload <bool>] [-ChatHistory <bool>] [-AllowedMembers <PSListModifier[string]>] [-DeniedMembers <PSListModifier[string]>] [-Creators <PSListModifier[string]>] [-WhatIf] [-Confirm]  [<CommonParameters>]

若要移除類別

    Remove-CsPersistentChatCategory -Instance <CategoryObject> [-Force <Switch Parameter>] [-Confirm <Switch Parameter>]

或

    Remove-CsPersistentChatCategory -Identity <String> [-Force <Switch Parameter>] [-Confirm <Switch Parameter>]

