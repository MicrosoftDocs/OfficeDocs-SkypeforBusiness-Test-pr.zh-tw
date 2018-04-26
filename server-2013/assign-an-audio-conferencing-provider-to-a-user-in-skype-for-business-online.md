---
title: 指派音訊會議提供者給使用者
TOCTitle: 指派音訊會議提供者給使用者
ms:assetid: 60db6896-9c5c-4d64-ab7e-10d91748587c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362791(v=OCS.15)
ms:contentKeyID: 56269092
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 指派音訊會議提供者給使用者

 

_**上次修改主題的時間：** 2015-06-22_

[Set-CsUserAcp](set-csuseracp.md) Cmdlet 可讓您將音訊會議提供者指派給使用者：

    Set-CsUserAcp -Identity "Ken Myer" -TollNumber "12065551219" -TollFreeNumbers "18005550712" -ParticipantPasscode "p@ssw0rd" -Domain "sip.contoso.com" -Name "Contoso ACP"

除非您與指定的提供者訂有合約，否則這項指派將無任何意義。

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

