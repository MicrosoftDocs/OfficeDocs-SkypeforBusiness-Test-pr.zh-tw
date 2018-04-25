---
title: 移除先前指派給使用者的音訊會議提供者
TOCTitle: 移除先前指派給使用者的音訊會議提供者
ms:assetid: 85d59e6c-d646-4908-9767-adb48763f6de
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362808(v=OCS.15)
ms:contentKeyID: 56269111
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移除先前指派給使用者的音訊會議提供者

 

_**上次修改主題的時間：** 2015-06-22_

若要移除指派給使用者的所有音訊會議提供者，請執行 [Remove-CsUserAcp](remove-csuseracp.md) Cmdlet 而不加入任何參數 (表示相關使用者的 Identity 參數除外)：

    Remove-CsUserAcp -Identity "Ken Myer"

如有多個音訊會議提供者指派給使用者，您可以加入 Name 參數，後接所要移除的提供者名稱，藉此移除單一提供者：

    Remove-CsUserAcp -Identity "Ken Myer" -Name "Contoso ACP"

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

