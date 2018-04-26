---
title: 已超過此租用戶的同時命令介面數上限
TOCTitle: 已超過此租用戶的同時命令介面數上限
ms:assetid: a4c91ffa-fdcc-414c-b941-a0d36c906825
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362832(v=OCS.15)
ms:contentKeyID: 56269137
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 已超過此租用戶的同時命令介面數上限

 

_**上次修改主題的時間：** 2015-06-22_

雖然每個系統管理員最多可允許同時有三個與 商務用 Skype Online 租用戶的連線，但任何一個租用戶均不得同時有超過九個連線。例如，三個系統管理員可能各有三個工作階段開啟。如果第四個系統管理員嘗試進行連線 (導致同時共有 10 個連線)，則這個連線嘗試將會失敗，並出現下列錯誤訊息：

    New-PSSession : [admin.vdomain.com] 連線到遠端伺服器 admin.vdomain.com 失敗，傳回下列錯誤訊息:WS-Management 服務無法處理該要求。已超過此租用戶的並行殼層上限。請關閉現有的殼層或提高此租用戶的配額。如需詳細資訊，請參閱＜about_Remote_Troubleshooting＞說明主題。.

若要解決此問題，唯一的做法是關閉一或多個先前的連線。完成 商務用 Skype Online 工作階段後，建議使用 **Remove-PSSession** Cmdlet 終止該工作階段，如此將有助您避免此問題發生。

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

