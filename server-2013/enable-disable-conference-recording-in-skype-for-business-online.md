---
title: 啟用/停用會議記錄
TOCTitle: 啟用/停用會議記錄
ms:assetid: f6c5afab-081c-495c-97f7-135dcc2f6085
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362857(v=OCS.15)
ms:contentKeyID: 56269168
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用/停用會議記錄

 

_**上次修改主題的時間：** 2015-06-22_

若是不希望使用者擁有線上會議記錄功能，請使用 [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md) Cmdlet 並將 AllowConferenceRecording 參數值設為 False ($False)：

    Set-CsMeetingConfiguration -AllowConferenceRecording $False

若要恢復線上會議記錄功能，請將 AllowConferenceRecording 參數值設為 True ($True)：

    Set-CsMeetingConfiguration -AllowConferenceRecording $True

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

