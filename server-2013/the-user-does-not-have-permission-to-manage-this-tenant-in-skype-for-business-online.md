---
title: 使用者沒有管理此租用戶的權限
TOCTitle: 使用者沒有管理此租用戶的權限
ms:assetid: 714ccf81-9451-4585-b62d-979f2a606315
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362812(v=OCS.15)
ms:contentKeyID: 56269115
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用者沒有管理此租用戶的權限

 

_**上次修改主題的時間：** 2015-06-22_

若要以 Windows PowerShell 遠端連線至 商務用 Skype Online，您必須為 Tenant Administrators 群組的成員。如果不是，您的連線嘗試將會失敗，並收到下列錯誤訊息：

    New-PSSession : [admin.vdomain.com] 處理來自遠端伺服器 admin.vdomain.com 的資料失敗，傳回下列錯誤訊息:使用者 'user@foo.com' 沒有權限可管理此租用戶。只要為使用者指派適當的 RBAC 角色，即可授予權限。如需詳細資訊，請參閱 about_Remote_Troubleshooting 說明主題。.

如果您認為您已是或應該是 Tenant Administrators 群組的成員，請連絡 Office 365 支援。

## 請參閱

#### 概念

[診斷並解決與 Lync Online 的連線問題](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

