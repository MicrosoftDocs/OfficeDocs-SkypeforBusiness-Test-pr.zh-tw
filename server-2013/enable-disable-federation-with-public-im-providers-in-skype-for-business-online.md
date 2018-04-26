---
title: 啟用/停用與公用 IM 提供者的同盟
TOCTitle: 啟用/停用與公用 IM 提供者的同盟
ms:assetid: 8609682c-97d3-48e6-a243-d84c1f9c8419
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362809(v=OCS.15)
ms:contentKeyID: 56269112
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用/停用與公用 IM 提供者的同盟

 

_**上次修改主題的時間：** 2015-06-22_

若要讓使用者得以與具有公用立即訊息 (IM) 提供者帳戶的使用者進行通訊，請使用 [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) Cmdlet 並將 AllowPublicUsers 屬性設為 True ($True)：

    Set-CsTenantFederationConfiguration -AllowPublicUsers $True

請注意，您接著必須使用 [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) Cmdlet 指定允許使用者與之通訊的公用 IM 提供者。

若要停用與公用提供者的同盟，請將 AllowPublicUsers 屬性設回 False ($False)：

    Set-CsTenantFederationConfiguration -AllowPublicUsers $False

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

