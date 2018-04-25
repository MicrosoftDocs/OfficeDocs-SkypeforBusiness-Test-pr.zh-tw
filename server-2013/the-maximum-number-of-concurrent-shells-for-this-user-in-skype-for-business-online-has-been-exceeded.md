---
title: 已超過此使用者的同時命令介面數上限
TOCTitle: 已超過此使用者的同時命令介面數上限
ms:assetid: b309efe8-a214-41ea-a345-93e6a36e0cb1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362837(v=OCS.15)
ms:contentKeyID: 56269143
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 已超過此使用者的同時命令介面數上限

 

_**上次修改主題的時間：** 2015-06-22_

每個系統管理員最多可允許同時擁有三個與 商務用 Skype Online 的遠端連線。若是您有三個 Windows PowerShell 遠端連線正在執行，要建立第四個同時連線的任何嘗試將會失敗，並出現下列錯誤訊息：

    New-PSSession : [admin.vdomain.com] 連線到遠端伺服器 admin.vdomain.com 失敗，傳回下列錯誤訊息:WS-Management 服務無法處理該要求。已超過此使用者的並行殼層最大數目。請關閉現有的殼層，或提高此使用者的配額。如需詳細資訊，請參閱 about_Remote_Troubleshooting 說明主題。

若要解決此問題，唯一的做法是關閉一或多個先前的連線。完成 商務用 Skype Online 工作階段後，建議使用 **Remove-PSSession** Cmdlet 終止工作階段，如此將有助您避免此問題發生。

## 請參閱

#### 概念

[診斷並解決與 Lync Online 的連線問題](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

