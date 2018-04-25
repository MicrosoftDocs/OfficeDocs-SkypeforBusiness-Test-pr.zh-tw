---
title: 啟用/停用 iPhone 與 Windows Phone 的推播通知
TOCTitle: 啟用/停用 iPhone 與 Windows Phone 的推播通知
ms:assetid: 64482dcb-6354-4fb5-a2e4-1564b3d0e047
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362792(v=OCS.15)
ms:contentKeyID: 56269094
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用/停用 iPhone 與 Windows Phone 的推播通知

 

_**上次修改主題的時間：** 2015-06-22_

若要停用推播通知傳送至 iPhone 或 Windows Phone，請使用 [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md) Cmdlet 並將 EnableApplePushNotificationService 與 EnableMicrosoftPushNotificationService 的屬性值設為 False ($False)：

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $False

請注意，iPhone 與 Windows Phone 可分開設定。例如，下列命令會停用 iPhone 上的推播通知，但會啟用 Windows Phone 上的推播通知：

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $True

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

