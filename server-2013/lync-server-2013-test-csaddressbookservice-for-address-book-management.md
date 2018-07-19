---
title: 適用於通訊錄管理的 Test-CsAddressBookService
TOCTitle: 適用於通訊錄管理的 Test-CsAddressBookService
ms:assetid: b88cea74-41fd-4c0e-9284-7135bff27a27
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429720(v=OCS.15)
ms:contentKeyID: 49292117
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 適用於通訊錄管理的 Test-CsAddressBookService

 

_**上次修改主題的時間：** 2012-11-01_

誰可以執行這個 Cmdlet：根據預設，會授權下列群組的成員執行 Test-CsAddressBookService Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中輸入下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Test-CsAddressBookService"}

Lync Server 2013 包含一些可起始綜合命令的 Cmdlet，用於確認特定函數或功能可正常運作。Test-CsAddressBookService 會確認定義的使用者可以連接通訊錄 Web 服務，並向該服務要求本機檔案。

例如：

    Test-CsAddressBookService -TargetFqdn atl-cs-001.contoso.com -UserCredential contoso\bob -UserSipAddress "sip:bob@contoso.com"

## 請參閱

#### 其他資源

[Test-CsAddressBookService](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsAddressBookService)

