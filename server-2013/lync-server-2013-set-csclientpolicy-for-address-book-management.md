---
title: 用於通訊錄管理的 Set-CsClientPolicy
TOCTitle: 用於通訊錄管理的 Set-CsClientPolicy
ms:assetid: e7788bea-606f-481a-a3a4-1855ac028493
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429723(v=OCS.15)
ms:contentKeyID: 49292654
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 用於通訊錄管理的 Set-CsClientPolicy

 

_**上次修改主題的時間：** 2012-11-01_

誰可以執行這個 Cmdlet：根據預設，下列群組成員已獲得授權，可在本機執行 Set-CsClientPolicy Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中輸入下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsClientPolicy"}

Set-CsClientPolicy Cmdlet 類似於 New-CsClientPolicy，可讓您修改已經存在的用戶端設定。

例如：

    Set-CsClientPolicy -Identity RedmondClientPolicy -WebServicePollInterval "00:15:00" -AddressBookAvailability "WebSearchAndFileDownload"

如需完整命令的詳細說明，請參閱主要 Lync Server Windows PowerShell RTCCmdlets 參考中的下列項目。

## 請參閱

#### 其他資源

[Set-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientPolicy)

