---
title: 管理增益集
TOCTitle: 管理增益集
ms:assetid: b84f868e-b36e-4ab4-b284-7db212d401c3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205193(v=OCS.15)
ms:contentKeyID: 49292101
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 管理增益集

 

_**上次修改主題的時間：** 2012-10-06_

建立新 常設聊天室伺服器 增益集

    New-CsPersistentChatAddin -Name Contoso -PersistentChatPoolFqdn client.contoso.com -Url http://contoso.com 

## 建立、取得、設定或移除增益集

建立新增益集

    New-CsPersistentChatAddin -PersistentChatPoolFqdn <String> -Name <String> -Url<String>

> [!IMPORTANT]  
> 只有在擁有一個以上的 Persistent Chat Server 集區時，才需要 PersistentChatPoolFqdn &lt;String&gt;。



取得增益集

    Get-CsPersistentChatAddin -Identity <String>]

或

    Get-CsPersistentChatAddin -PersistentChatPoolFqdn <String>

設定增益集

    Set-CsPersistentChatAddIn -Instance <AddinObject> [-Force <Switch Parameter>] [-Confirm <Switch Parameter>]

或

    Set-CsPersistentChatAddIn -Identity <String> [-Name <String>] [-Url<String>] [-Force <Switch Parameter>] [-Confirm <Switch Parameter>]

移除增益集

    Remove-CsPersistentChatAddIn -Instance <AddinObject> [-Force <Switch Parameter>] [-Confirm <Switch Parameter>]

或

    Remove-CsPersistentChatAddIn -Identity <String> [-Force <Switch Parameter>] [-Confirm <Switch Parameter>]

