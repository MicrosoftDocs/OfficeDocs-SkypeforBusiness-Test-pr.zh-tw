---
title: 由 Windows PowerShell 版本錯誤所導致的 Import-Module 錯誤
TOCTitle: 由 Windows PowerShell 版本錯誤所導致的 Import-Module 錯誤
ms:assetid: 6c209f41-2b97-4dda-b0b7-e5b582d3e6b6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362802(v=OCS.15)
ms:contentKeyID: 56269104
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 由 Windows PowerShell 版本錯誤所導致的 Import-Module 錯誤

 

_**上次修改主題的時間：** 2015-06-22_

商務用 Skype Online Connector 模組僅可以 Windows PowerShell 3.0 執行。若是嘗試以舊版的 Windows PowerShell 匯入模組，匯入程序將會失敗，並出現類似下列的錯誤訊息：

    Import-Module : 載入的 PowerShell 版本是 '2.0'。模組 'D:\Program Files\Common Files\Microsoft Lync Server 2013\Modules\LyncOnlineConnector\LyncOnlineConnector.psd1' 需要至少 PowerShell '3.0' 版才能執行。請確認 PowerShell 安裝，然後再試一次。

若要修正此問題，唯一的做法是安裝 Windows PowerShell 3.0，該程式可透過 Microsoft 下載中心取得：<http://www.microsoft.com/en-us/download/details.aspx?id=29939>。

## 請參閱

#### 概念

[診斷並解決與 Lync Online 的連線問題](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

