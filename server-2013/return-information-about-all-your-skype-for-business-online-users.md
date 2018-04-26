---
title: 傳回所有 Lync Online 使用者的相關資訊
TOCTitle: 傳回所有 Lync Online 使用者的相關資訊
ms:assetid: 0b59fadf-67e6-48ea-86f1-2efef500ebdf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362769(v=OCS.15)
ms:contentKeyID: 56269067
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 傳回所有 Lync Online 使用者的相關資訊

 

_**上次修改主題的時間：** 2015-06-22_

若要傳回已啟用 商務用 Skype Online 之所有使用者的相關資訊，請呼叫 [Get-CsOnlineUser](get-csonlineuser.md) Cmdlet，無需加入任何額外參數：

    Get-CsOnlineUser

若要傳回隨機選取的單一使用者 (例如將該帳號用於測試目的)，請呼叫 **Get-CsOnlineUser** Cmdlet 並將 ResultSize 參數設為 1：

    Get-CsOnlineUser -ResultSize 1

如此一來，無論組織中的使用者人數多少，**Get-CsOnlineUser** Cmdlet 僅會傳回單一使用者的相關資訊。若要傳回五名使用者的相關資訊，請將 ResultSize 參數值設為 5：

    Get-CsOnlineUser -ResultSize 5

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

