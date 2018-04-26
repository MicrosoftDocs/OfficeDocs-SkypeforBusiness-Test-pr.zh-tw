---
title: 參數 vs. 屬性
TOCTitle: 參數 vs. 屬性
ms:assetid: 65348f95-f4d4-40cd-8869-f9d72643792d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362796(v=OCS.15)
ms:contentKeyID: 56269098
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 參數 vs. 屬性

 

_**上次修改主題的時間：** 2015-06-22_

檢閱 商務用 Skype Online Cmdlet 的說明主題時，有時您會看到「參數」與「屬性」兩個詞彙交替互用。千萬別被這些術語給搞混了：雖然就技術上來說，兩者有所差異，但在 商務用 Skype Online 中，兩者基本上並無不同。

就技術上來說，執行 Cmdlet 時使用的是參數。例如，在下列 Windows PowerShell 命令中，EnableMicrosoftPushNotificationService 與 EnableApplePushNotificationService 均為 [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md) Cmdlet 的參數：

    Set-CsPushNotificationConfiguration -EnableMicrosoftPushNotificationService -EnableApplePushNotificationService $True

屬性則是 商務用 Skype Online 物件的屬性 (例如推播通知組態設定的集合)。假設您執行下列命令：

    Set-CsPushNotificationConfiguration

執行此操作後，您將會收到屬性與其關聯值的集合，其中將包含下列項目：

    EnableMicrosoftPushNotificationService : True
    EnableApplePushNotificationService     : True

如您所見，屬性與參數共用相同的名稱：您使用 EnableMicrosoftPushNotificationService 參數設定 EnableMicrosoftPushNotificationService 的屬性值。

## 請參閱

#### 概念

[Windows PowerShell 與 Lync Online 的簡介](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

