---
title: 傳回特定使用者的相關資訊
TOCTitle: 傳回特定使用者的相關資訊
ms:assetid: 6c8c2190-8e62-4f92-bbe9-4f692bd7ebf5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362803(v=OCS.15)
ms:contentKeyID: 56269105
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 傳回特定使用者的相關資訊

 

_**上次修改主題的時間：** 2015-06-22_

呼叫 [Get-CsOnlineUser](get-csonlineuser.md) Cmdlet 時有數種方式可參照至特定使用者帳戶。您可以採用使用者的 Active Directory 網域服務顯示名稱：

    Get-CsOnlineUser -Identity "Ken Myer"

您可以採用使用者的 SIP 位址：

    Get-CsOnlineUser -Identity "sip:kenmyer@litwareinc.com"

您可以採用使用者的主體名稱 (UPN)：

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

