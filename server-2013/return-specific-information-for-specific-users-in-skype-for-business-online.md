---
title: 傳回特定使用者的特定資訊
TOCTitle: 傳回特定使用者的特定資訊
ms:assetid: bbee85bd-d8a7-4b28-90d7-45c43eee48f6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362838(v=OCS.15)
ms:contentKeyID: 56269145
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 傳回特定使用者的特定資訊

 

_**上次修改主題的時間：** 2015-06-22_

根據預設，[Get-CsOnlineUser](get-csonlineuser.md) Cmdlet 會傳回各個 商務用 Skype Online 使用者帳戶的大量資訊。若是僅需部分資訊，請將傳回資料傳送至 **Select-Object** Cmdlet。例如，下列命令會傳回使用者 Ken Myer 的所有相關資料，然後使用 **Select-Object** Cmdlet 將畫面上的顯示資訊限制為 Ken 的 Active Directory 網域服務顯示名稱與撥號對應表：

    Get-CsOnlineUser -Identity "Ken Myer" | Select-Object DisplayName, DialPlan

下列命令會為您的所有使用者傳回顯示名稱與撥號對應表。

    Get-CsOnlineUser | Select-Object DisplayName, DialPlan

若要尋找 商務用 Skype Online 使用者帳戶的內容，請使用下列命令：

    Get-CsOnlineUser | Get-Member

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

