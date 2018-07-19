---
title: 適用於通訊錄管理的 Set-CsAddressBookConfiguration
TOCTitle: 適用於通訊錄管理的 Set-CsAddressBookConfiguration
ms:assetid: 3a64ceb1-9f79-4f3b-bf33-eaf346dbd60d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429700(v=OCS.15)
ms:contentKeyID: 49290634
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 適用於通訊錄管理的 Set-CsAddressBookConfiguration

 

_**上次修改主題的時間：** 2012-11-01_

誰可以執行這個 Cmdlet：根據預設，下列群組的成員已獲得授權，可在本機執行 Set-CsAddressBookConfiguration Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中輸入下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsAddressBookConfiguration"}

Set-CsAddressBookConfiguration 類似於 new-csaddressbookconfiguration Cmdlet，但前者是用來修改現有設定。

例如：

    Set-CsAddressBookConfiguration -identity site:Redmond -RunTimeOfDay 23:00

如需完整命令的詳細說明，請參閱主要 Lync Server Windows PowerShell RTCCmdlets 參考中的下列項目。

## 請參閱

#### 其他資源

[Set-CsAddressBookConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsAddressBookConfiguration)

