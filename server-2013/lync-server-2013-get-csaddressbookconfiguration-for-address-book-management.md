---
title: 用於通訊錄管理的 Get-CsAddressBookConfiguration
TOCTitle: 用於通訊錄管理的 Get-CsAddressBookConfiguration
ms:assetid: bd62f916-caf3-4e10-ada4-631bbb331ef1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429721(v=OCS.15)
ms:contentKeyID: 49292146
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 用於通訊錄管理的 Get-CsAddressBookConfiguration

 

_**上次修改主題的時間：** 2012-11-01_

誰可以執行這個 Cmdlet：根據預設，會授權下列群組的成員在本機執行 Get-CsAddressBookConfiguration Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中輸入下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Get-CsAddressBookConfiguration"}

Get-CsAddressBookConfiguration Cmdlet 會傳回已存在之設定的相關資訊。

例如：

    Get-CsAddressBookConfiguration -Identity site:Redmond

結合 Get-CsAddressBookConfiguration 和 Set-CsAddressBookConfiguration 的功能後，可讓系統管理員定義要修改的設定，然後套用修改。例如，此結合項目：

    Get-CsAddressBookConfiguration -Filter site:* | Set-CsAddressBookConfiguration -RunTimeOfDay 23:00

傳回所有網站中的所有設定，並將 23:00 小時的 RunTimeOfDay 套用至設定。

如需完整命令的詳細說明，請參閱主要 Lync Server Windows PowerShell RTCCmdlets 參考中的下列項目。

## 請參閱

#### 其他資源

[Get-CsAddressBookConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsAddressBookConfiguration)

