---
title: 防止匿名使用者獲准自動進入會議
TOCTitle: 防止匿名使用者獲准自動進入會議
ms:assetid: 23f120d2-4c39-4509-aa1f-4d186a525075
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362775(v=OCS.15)
ms:contentKeyID: 56269073
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 防止匿名使用者獲准自動進入會議

 

_**上次修改主題的時間：** 2015-06-22_

若要防止匿名使用者自動獲准加入線上會議，請使用 [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md) Cmdlet，並將 AdmitAnonymousUsersByDefault 屬性設為 False ($False)：

    Set-CsMeetingConfiguration -AdmitAnonymousUsersByDefault $False

若要啟用自動准許功能，請將 AdmitAnonymousUsersByDefault 屬性設回 True ($True)：

    Set-CsMeetingConfiguration -AdmitAnonymousUsersByDefault $True

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

