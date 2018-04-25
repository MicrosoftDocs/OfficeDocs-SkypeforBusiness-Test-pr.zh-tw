---
title: 檢視推播通知設定的相關資訊
TOCTitle: 檢視推播通知設定的相關資訊
ms:assetid: be5c6b01-4294-4d17-9772-fed40201e8a5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721868(v=OCS.15)
ms:contentKeyID: 49890287
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視推播通知設定的相關資訊

 

_**上次修改主題的時間：** 2013-02-23_

推入通知 (其格式包括徽章、圖示或通知) 可傳送至行動裝置，即使行動應用程式非作用中亦然。推入通知會通知使用者新的或未接的 IM 邀請和語音信箱等事件。您可使用 Lync Server 2013 控制台 或 Lync Server 2013 管理命令介面，檢視行動裝置推入通知設定的相關資訊。

## 從 Lync Server 控制台檢視推入通知

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[用戶端\]，然後按一下 \[推入通知設定\] 導覽按鈕。

4.  在 \[推入通知設定\] 頁面上，依序按一下您要檢視的網站、\[編輯\] 功能表及 \[顯示詳細資料\]。

## 使用 Windows PowerShell Cmdlet 檢視推入通知設定資訊

您也可以使用 Lync Server 管理命令介面和 **Get-CsPushNotificationConfiguration** Cmdlet 檢視推入通知設定資訊。您可從 Lync Server 2013 管理命令介面或 Windows PowerShell. 如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。 的遠端工作階段執行此 Cmdlet

## 檢視推入通知設定資訊

  - 若要檢視您的推入通知設定相關資訊，請在 Lync Server 管理命令介面 中輸入下列命令，然後按 ENTER 鍵：
    
        Get-CsPushNotificationConfiguration
    
    接著會傳回類似下方的資訊：
    
        Identity                               : Global
        EnableApplePushNotificationService     : False
        EnableMicrosoftPushNotificationService : False

如需詳細資訊，請參閱 [Get-CsPushNotificationConfiguration](get-cspushnotificationconfiguration.md) Cmdlet 的說明主題。

## 請參閱

#### 工作

[在 Lync Server 2013 中設定推播通知](lync-server-2013-configuring-for-push-notifications.md)

