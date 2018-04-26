---
title: Lync Server 2013：設定常設聊天室伺服器
TOCTitle: 設定常設聊天室伺服器
ms:assetid: 85028aff-a38e-4748-958e-59e707a47532
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205054(v=OCS.15)
ms:contentKeyID: 49291544
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定常設聊天室伺服器

 

_**上次修改主題的時間：** 2012-10-06_

建立新的 常設聊天室設定

    New-CsPersistentChatConfiguration -Identity <XdsIdentity> [-DefaultChatHistory <Integer>] [-MaxChatContentSizeMB <Integer>] [-MaxFileSizeKB <Integer>] [-ParticipantUpdateLimit <Integer>] [-FileServiceUrl <UrlForFileUpload>] [-RoomManagementUrl <RoomManagementUrl>] [-Instance <PSObject>] [-Force <Switch Parameter>] [-Confirm <Switch Parameter>] [-WhatIf <Switch Parameter>]

取得 常設聊天室設定

    Get-CsPersistentChatConfiguration [-LocalStore <Switch Parameter>] [-Identity <XdsIdentity>]

移除 常設聊天室設定

    Remove-CsPersistentChatConfiguration -Identity <XdsIdentity>

設定 常設聊天室設定

    Set-CsPersistentChatConfiguration [-DefaultChatHistory <Integer>] [-MaxChatContentSizeMB <Integer>] [-MaxFileSizeKB <Integer>] [-ParticipantUpdateLimit <Integer>] [-FileServiceUrl <UrlForFileUpload>] [-RoomManagementUrl <RoomManagementUrl>] [-Instance <PSObject >] [-Force <Switch Parameter>] [-Confirm <Switch Parameter>] [-WhatIf <Switch Parameter>]

對於 Lync Server 2013， 前端伺服器的 Lync Server 2013 支援所有 Web 服務流量。因此，不需要 常設聊天室伺服器 的 gcweb01 位址。我們仍然支援內部 Web 服務，因為我們只為「內部」 網站提供檔案上傳/下載 Web 服務 (對於遠端使用者的 *外部* 網站則不提供)。

