---
title: 用於通訊錄管理的 new-csaddressbookconfiguration
TOCTitle: 用於通訊錄管理的 new-csaddressbookconfiguration
ms:assetid: a58ddc8c-ae04-4141-b69e-e45374a67d72
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429718(v=OCS.15)
ms:contentKeyID: 49291897
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 用於通訊錄管理的 new-csaddressbookconfiguration

 

_**上次修改主題的時間：** 2012-11-01_

誰可以執行這個 Cmdlet：根據預設，下列群組成員已獲得授權，可在本機上執行 new-csaddressbookconfiguration Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中輸入下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "new-csaddressbookconfiguration"}

new-csaddressbookconfiguration Cmdlet 會建立新設定來管理通訊錄的行為。這個 Cmdlet 的特殊之處在於能夠定義通訊錄服務是否建立用戶端下載檔、是否使用正規化規則以及如何使用、保留 delta 和小型 delta 檔的時間、整合新的完整檔案建立之前的 delta 檔大小、一天中建立完整通訊錄檔案的時間，以及在使用者資料庫中同步資訊的內部應該為何。

例如：

    new-csaddressbookconfiguration -Identity site:Redmond -KeepDuration 15 -SynchronizePollingInterval 00:10:00

如需完整命令的詳細說明，請參閱主要 Lync Server Windows PowerShell RTCCmdlets 參考中的下列項目。

## 請參閱

#### 其他資源

[new-csaddressbookconfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsAddressBookConfiguration)

