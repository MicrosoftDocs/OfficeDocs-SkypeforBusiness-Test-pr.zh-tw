---
title: 用於通訊錄管理的 New-CsClientPolicy
TOCTitle: 用於通訊錄管理的 New-CsClientPolicy
ms:assetid: ef4415fc-82c4-4dc8-97d1-37a084553343
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429726(v=OCS.15)
ms:contentKeyID: 49292748
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 用於通訊錄管理的 New-CsClientPolicy

 

_**上次修改主題的時間：** 2012-11-01_

誰可以執行這個 Cmdlet：根據預設，下列群組成員已獲得授權，可執行 New-CsClientPolicy Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中輸入下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "New-CsClientPolicy"}

Cmdlet New-CsClientPolicy 會針對 Lync Server 2013 提供的功能，定義用於佈建用戶端的大量設定。若為通訊錄服務，則是 AddressBookAvailability 參數。這個參數會直接影響用戶端可用的選項，包括下列三個選項：

  - WebSearchAndFileDownload

  - WebSearchOnly

  - FileDownloadOnly

若定義，它會決定用戶端存取通訊錄的方式。如果您定義這個參數，則必須定義其中一個選項。如果您未修改這項設定，則預設的 WebSearchAndFileDownload 會持續有效。

例如：

    New-CsClientPolicy -Identity RedmondClientPolicy -DisableCalendarPresence $True -DisablePhonePresence $True -DisplayPhoto "PhotosFromADOnly" -AddressBookAvailability "WebSearchOnly"

## 請參閱

#### 其他資源

[New-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClientPolicy)

