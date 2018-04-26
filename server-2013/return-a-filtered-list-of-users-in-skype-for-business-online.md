---
title: 傳回使用者的篩選清單
TOCTitle: 傳回使用者的篩選清單
ms:assetid: f2c4d13b-8601-4192-8b94-e9a57969da11
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362858(v=OCS.15)
ms:contentKeyID: 56269169
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 傳回使用者的篩選清單

 

_**上次修改主題的時間：** 2015-06-22_

藉由使用 [Get-CsOnlineUser](get-csonlineuser.md) Cmdlet 搭配 LdapFilter 或 Filter 參數，您可以輕鬆傳回目標使用者的相關資訊。例如，下列命令可傳回在財務部門工作的所有使用者：

    Get-CsOnlineUser -LdapFilter "department=Finance"

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

