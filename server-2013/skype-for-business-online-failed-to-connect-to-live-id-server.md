---
title: Live ID Server 連線失敗
TOCTitle: Live ID Server 連線失敗
ms:assetid: 701af721-dd6a-4f48-96f9-94e89c644201
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362811(v=OCS.15)
ms:contentKeyID: 56269114
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Live ID Server 連線失敗

 

_**上次修改主題的時間：** 2015-06-22_

通常連線嘗試失敗並出現下列錯誤訊息的可能原因有三：

    Get-CsWebTicket : 無法連線至 Live ID 伺服器。請確定已啟用 Proxy，或電腦有網路連線可連線至 Live ID 伺服器。

此錯誤通常代表 Microsoft Online Services 登入小幫手並未執行。若要確認此服務的狀態，請從 Windows PowerShell 命令提示字元中執行下列命令：

    Get-Service "msoidsvc"

若是服務並未執行，請使用下列命令啟動服務：

    Start-Service "msoidsvc"

若是服務正在執行，您的電腦與 Microsoft Live ID 驗證伺服器之間可能發生網路連線問題。若要檢查連線是否發生問題，請開啟 Internet Explorer 並導覽至 <https://login.microsoftonline.com/>，然後嘗試從該處登入 Office 365。如果失敗，網路連線可能發生問題。

比較罕見的情況是 Microsoft Live ID 驗證伺服器的連線 URI 值設定錯誤。若已確認登入小幫手正在執行且網路連線正常，則這可能就是問題所在。倘若如此，請聯絡 Office 365 支援。

## 請參閱

#### 概念

[診斷並解決與 Lync Online 的連線問題](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

