---
title: 用於通訊錄管理的 Test-CsAddressBookWebQuery
TOCTitle: 用於通訊錄管理的 Test-CsAddressBookWebQuery
ms:assetid: 977a9c1f-5f4e-4539-9a26-8748b61a57d8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429716(v=OCS.15)
ms:contentKeyID: 49291731
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 用於通訊錄管理的 Test-CsAddressBookWebQuery

 

_**上次修改主題的時間：** 2012-11-01_

誰可以執行這個 Cmdlet：根據預設，以下群組的成員能取得在本機執行 Test-CsAddressBookWebQuery Cmdlet 的權限：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中輸入下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Test-CsAddressBookService"}

Test-CsAddressBookWebQuery 和 Test-CsAddressBookService 綜合交易相似，能針對通訊錄 Web 查詢來執行查詢以確保其正常運作。Cmdlet 會連接 Web 票證驗證及提供 –UserCredential 中指定的認證。如果通過驗證，Cmdlet 接著會提供 –TargetSipAddress 資訊。如果 Cmdlet 能擷取連絡人的相關資訊，它應會報告成功的結果。

例如：

    Test-CsAddressBookWebQuery -TargetFqdn atl-cs-001.contoso.com -UserCredential contoso\bob -UserSipAddress "sip:bob@contoso.com" -TargetSipAddress "sip:bob@contoso.com"

如需完整命令的詳細說明，請參閱主要 Lync Server Windows PowerShell RTCCmdlets 參考中的下列項目。

## 請參閱

#### 其他資源

[Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)

