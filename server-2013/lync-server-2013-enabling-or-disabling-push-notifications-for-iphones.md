---
title: 啟用或停用 iPhone 的推播通知
TOCTitle: 啟用或停用 iPhone 的推播通知
ms:assetid: 8bbf531a-807f-4a8f-814a-94bfed8f97ef
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688122(v=OCS.15)
ms:contentKeyID: 49890194
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用或停用 iPhone 的推播通知

 

_**上次修改主題的時間：** 2013-02-23_

推入通知 (其格式包括徽章、圖示或通知) 可傳送至 iPhone，即使行動應用程式非作用中亦然。推入通知會通知使用者新的或未接的 IM 邀請和語音信箱等事件。您可以使用 Lync Server 2013 控制台或 Lync Server 2013 管理命令介面，來啟用或停用 iPhone 的推入通知。

## 從 Lync Server 控制台啟用 iPhone 的推入通知

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[用戶端\]，然後按一下 \[推入通知設定\] 導覽按鈕。

4.  在 \[推入通知設定\] 頁面中，依序按一下您要編輯的網站、\[編輯\] 功能表及 \[顯示詳細資料\]。

5.  按一下 \[啟用 Apple 推入通知\] 核取方塊。

6.  按一下 \[認可\]。

## 從 Lync Server 控制台停用 iPhone 的推入通知

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[用戶端\]，然後按一下 \[推入通知設定\] 導覽按鈕。

4.  在 \[推入通知設定\] 頁面中，依序按一下您要編輯的網站、\[編輯\] 功能表及 \[顯示詳細資料\]。

5.  清除 \[啟用 Apple 推入通知\] 核取方塊。

6.  按一下 \[認可\]。

## 使用 Windows PowerShell Cmdlet 啟用或停用對 iPhone 的推入通知

您可以使用 **Set-CsPushNotificationConfiguration** Cmdlet，啟用或停用對 Apple iPhone 的推入通知。您可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 啟用 iPhone 的推入通知

  - 若要啟用 iPhone 的推入通知，請將 EnableApplePushNotificationService 屬性的值設定為 True ($True)。例如：
    
        Set-CsPushNotificationConfiguration -Identity "site:Redmond" -EnableApplePushNotificationService $True

## 停用 iPhone 的推入通知

  - 若要停用 iPhone 的推入通知，請將 EnableApplePushNotificationService 屬性的值設定為 False ($False)。例如：
    
        Set-CsPushNotificationConfiguration -Identity "site:Redmond" -EnableApplePushNotificationService $False

如需詳細資訊，請參閱適用於 [Set-CsPushNotificationConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsPushNotificationConfiguration) Cmdlet 的說明主題。

## 請參閱

#### 工作

[在 Lync Server 2013 中設定推播通知](lync-server-2013-configuring-for-push-notifications.md)

