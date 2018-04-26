---
title: 傳回指派給使用者之音訊會議提供者的相關資訊
TOCTitle: 傳回指派給使用者之音訊會議提供者的相關資訊
ms:assetid: 7fae822f-9f6c-4381-95c5-879661027925
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362814(v=OCS.15)
ms:contentKeyID: 56269116
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 傳回指派給使用者之音訊會議提供者的相關資訊

 

_**上次修改主題的時間：** 2015-06-22_

若要傳回指派給使用者的音訊會議提供者相關資訊，請使用 [Get-CsUserAcp](get-csuseracp.md) Cmdlet 與下列語法：

    Get-CsUserAcp -Identity "Ken Myer" | Select-Object -ExpandProperty AcpInfo

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

