---
title: 管理聊天室
TOCTitle: 管理聊天室
ms:assetid: d4835cf4-cd09-4769-a08e-e92706861b64
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205292(v=OCS.15)
ms:contentKeyID: 49292441
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 管理聊天室

 

_**上次修改主題的時間：** 2013-02-21_

建立新的 常設聊天室伺服器 聊天室

    New-CsPersistentChatRoom -Name Foo1 -PersistentChatPoolFqdn client.contoso.com -Category client.contoso.com\Foo [other parameters]

> [!IMPORTANT]  
> -如果下列其中一項條件為真，就不需要 PersistentChatPoolFqdn：
> <ul>
> <li><p>只有一個 Persistent Chat Server 集區。</p></li>
> <li><p>您對類別提供一個集區 FQDN。</p></li>
> <li><p>您提供集區 FQDN 來新增聊天室。</p></li>
> </ul>

對現有 常設聊天室伺服器 聊天室做出變更

    Set-CsPersistentChatRoom -Identity testCat -Members @{Add="sip:user1@contoso.com", "CN=container,DC=contoso,DC=com"}
    Set-CsPersistentChatRoom -Identity testCat -Managers @{Add="sip:user2@contoso.com"}
    Set-CsPersistentChatRoom -Identity testCat -Presenters @{Add="sip:user1@contoso.com"}

Windows PowerShell：可以同時設定成員、管理員及簡報者。其應該全是主機類別的 AllowedMembers 減去 DeniedMembers 後的子集。type=normal 的聊天室不可包含簡報者。

## 建立、取得、設定、清除或移除聊天室

建立新的聊天室

    New-CsPersistentChatRoom -Name <String> [-PersistentChatPoolFqdn <String>]-Category <String> [-Description <String>] [-Disabled <Switch Parameter>] [-Type <Normal | Auditorium>] [-AddIn <String>] [-Privacy <ChatRoomPrivacy> {Open | Closed | Secret}] [-Invitations <Switch Parameter>]

設定聊天室

    Set-CsPersistentChatRoom -Identity <String> [-Name <String>] [-Category <String>] [-Description <String>] [-Disabled <boolean>] [-Type <Normal | Auditorium>] [-AddIn <String>] [-Privacy <ChatRoomPrivacy> {Open | Closed | Secret}] [-Invitations <Enum>] [-Members <PSListModifier<String>>] [-Managers <PSListModifier<String>>] [-Presenters <PSListModifier<String>>] [-Force < Switch Parameter >] [-Confirm <Switch Parameter>][-WhatIf <Switch Parameter>]

取得聊天室

    Get-CsPersistentChatRoom -Identity <String>

或

    Get-CsPersistentChatRoom -filter <String> [-PersistentChatPoolFqdn <String>] [-SearchDescription] [-Member <String>] [-Manager <string>] [-Category <string>] [-Addin <string>] [-Disabled <bool>] [-Privacy <ChatRoomPrivacy> {Open | Closed | Secret}] [-Type <ChatRoomType> {Normal | Auditorium}] [-Invitations <ChatRoomInvitations> {False | Inherit}] [-ChatContentExceedsMB <int>] [-ResultSize <int>]

其中 –filter 只支援「名稱」及「描述」，且可幫助您找出名稱/描述符合關鍵字字串的聊天室。PoolFqdn 會在指定的Persistent Chat Server 集區中進行搜尋。

清除聊天室和清除聊天室的訊息

    Clear-CsPersistentChatRoom [-Identity] <string> -EndDate <DateTime> [-WhatIf] [-Confirm]  [<CommonParameters>]

或

    Clear-CsPersistentChatRoom [-Instance] <ChatRoomObject> -EndDate <DateTime> [-WhatIf] [-Confirm] [<CommonParameters>]

移除聊天室

    Remove-CsPersistentChatRoom [-Identity] <string> [-Force] [-WhatIf] [-Confirm]  [<CommonParameters>]

或

    Remove-CsPersistentChatRoom [-Instance] <ChatRoomObject> [-Force] [-WhatIf] [-Confirm]  [<CommonParameters>]

