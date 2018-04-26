---
title: 將先前指派給使用者的個別使用者原則取消指派
TOCTitle: 將先前指派給使用者的個別使用者原則取消指派
ms:assetid: bdba1d22-28e4-4203-a109-a3fb408783d3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362840(v=OCS.15)
ms:contentKeyID: 56269147
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將先前指派給使用者的個別使用者原則取消指派

 

_**上次修改主題的時間：** 2015-06-22_

若要將先前指派給使用者的個別使用者原則取消指派，請重新執行適當的 **Grant-Cs** Cmdlet (例如用於將語音原則取消指派的 [Grant-CsVoicePolicy](grant-csvoicepolicy.md) Cmdlet)，然後將 PolicyName 參數設為 Null 值 ($Null)：

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName $Null

若要取消指派您的所有使用者的語音原則，請使用下列命令：

    Get-CsOnlineUser | Grant-CsVoicePolicy -PolicyName $Null

將使用者的原則取消指派後，該使用者將受全域原則管理。

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

