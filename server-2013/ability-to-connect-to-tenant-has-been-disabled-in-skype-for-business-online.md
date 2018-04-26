---
title: 連線至租用戶的功能已遭停用
TOCTitle: 連線至租用戶的功能已遭停用
ms:assetid: 7365d31b-173e-4339-b0a3-98ab73a9558f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362820(v=OCS.15)
ms:contentKeyID: 56269124
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 連線至租用戶的功能已遭停用

 

_**上次修改主題的時間：** 2015-06-22_

若要使用 Windows PowerShell 管理 商務用 Skype Online，您的租用戶 Windows PowerShell 原則的 EnableRemotePowerShellAccess 屬性必須設為 True。如果不是，您的連線將會失敗，並收到下列錯誤訊息：

    New-PSSession : [admin.vdomain.com] 處理來自遠端伺服器 admin.vdomain.com 的資料失敗，傳回下列錯誤訊息:使用遠端 PowerShell 工作階段連線至此租用戶的功能已停用。請連絡 Lync 服務人員，以檢查此租用戶的租用戶 Powershell 原則。如需詳細資訊，請參閱 about_Remote_Troubleshooting 說明主題。.

若是出現此錯誤訊息，請連絡 Office 365 支援並啟用遠端 Windows PowerShell 存取。

## 請參閱

#### 概念

[診斷並解決與 Lync Online 的連線問題](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

