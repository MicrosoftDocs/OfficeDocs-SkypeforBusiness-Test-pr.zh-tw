---
title: Lync Server 2013：執行、授與、取得、移除或設定常設聊天室原則
TOCTitle: 執行、授與、取得、移除或設定常設聊天室原則
ms:assetid: 39ccdbe8-fb3d-47bc-96e2-9486b6d317e0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204810(v=OCS.15)
ms:contentKeyID: 49290630
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中執行、授與、取得、移除或設定常設聊天室原則

 

_**上次修改主題的時間：** 2012-10-01_

建立新的 常設聊天室原則

    New-CsPersistentChatPolicy -Identity <XdsIdentity> [-Enable <Switch Parameter>] [-Confirm <Switch Parameter>] [-Force <Switch Parameter>] [-WhatIf <Switch Parameter>] [-InMemory <Switch Parameter>]

授與 常設聊天室原則

    Grant-CsPersistentChatPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm <Switch Parameter>] [-WhatIf <Switch Parameter>]

取得 常設聊天室原則

    Get-CsPersistentChatPolicy [-Identity <XdsIdentity>] [-Filter <String>] [-LocalStore <Switch Parameter>]

移除 常設聊天室原則

    Remove-CsPersistentChatPolicy -Identity <XdsIdentity> [-Confirm <Switch Parameter>] [-Force <Switch Parameter>] [-WhatIf <Switch Parameter>]

設定 常設聊天室原則

    Set-CsPersistentChatPolicy [-Identity <XdsIdentity>] [-Instance < PSObject>]

