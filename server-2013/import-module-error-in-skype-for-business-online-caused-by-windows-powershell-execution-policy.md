---
title: 由 Windows PowerShell 執行原則所導致的 Import-Module 錯誤
TOCTitle: 由 Windows PowerShell 執行原則所導致的 Import-Module 錯誤
ms:assetid: 4bc093ca-fd30-44c9-a0a3-16f78698df2b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362786(v=OCS.15)
ms:contentKeyID: 56269086
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 由 Windows PowerShell 執行原則所導致的 Import-Module 錯誤

 

_**上次修改主題的時間：** 2015-06-22_

Windows PowerShell 執行原則可協助判定可載入 Windows PowerShell 主控台的設定檔，以及使用者可從主控台執行的指令碼。除非執行原則至少已設為 RemoteSigned，否則無法匯入 商務用 Skype Online 連接器模組。如果沒有設為 RemoteSigned，您將會在嘗試匯入模組時收到下列錯誤訊息：

    Import-Module : 因為這個系統上已停用指令碼執行，所以無法載入 C:\Program Files\Common Files\Microsoft Lync Server 2013\Modules\LyncOnlineConnector\LyncOnlineConnectorStartup.psm1 檔案。如需詳細資訊，請參閱＜about_Execution_Policies＞，網址為 http://go.microsoft.com/fwlink/?LinkID=135170。

若要解決此問題，請以系統管理員身分啟動 Windows PowerShell，然後執行下列命令：

    Set-ExecutionPolicy RemoteSigned

如需有關執行原則的詳細資訊，請參閱說明主題：[http://go.microsoft.com/fwlink/?LinkID=135170](http://go.microsoft.com/fwlink/?linkid=135170)。

## 請參閱

#### 概念

[診斷並解決與 Lync Online 的連線問題](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

