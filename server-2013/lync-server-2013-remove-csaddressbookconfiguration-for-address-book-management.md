---
title: 適用於通訊錄管理的 Remove-CsAddressBookConfiguration
TOCTitle: 適用於通訊錄管理的 Remove-CsAddressBookConfiguration
ms:assetid: 5d173ebe-ec4d-4640-8432-a25071ea9cc5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429705(v=OCS.15)
ms:contentKeyID: 49291050
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 適用於通訊錄管理的 Remove-CsAddressBookConfiguration

 

_**上次修改主題的時間：** 2012-11-01_

誰可以執行這個 Cmdlet：根據預設，會授權下列群組的成員在本機執行 Remove-CsAddressBookConfiguration Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中輸入下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Remove-CsAddressBookConfiguration"}

Remove-CsAddressBookConfiguration 會名符其實地依據定義的 Site Identity 移除組態。

例如：

    Remove-CsAddressBookConfiguration -Identity site:Redmond

如需完整命令的詳細說明，請參閱主要 Lync Server Windows PowerShell RTCCmdlets 參考中的下列項目。

## 請參閱

#### 其他資源

[Remove-CsAddressBookConfiguration](remove-csaddressbookconfiguration.md)

