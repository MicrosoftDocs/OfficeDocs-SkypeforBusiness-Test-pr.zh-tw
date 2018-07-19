---
title: 確認已移除舊版集區中的所有 Exchange UM 連絡人物件
TOCTitle: 確認已移除舊版集區中的所有 Exchange UM 連絡人物件
ms:assetid: 5a813169-0ed7-4f84-a242-ed2cd4ea5c43
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688068(v=OCS.15)
ms:contentKeyID: 49890082
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 確認已移除舊版集區中的所有 Exchange UM 連絡人物件

 

_**上次修改主題的時間：** 2012-09-26_

使用 **OCSUmUtil** 工具或 **Get-CsExumContact** Cmdlet，來驗證 Exchange UM 連絡人物件是否已從舊版 Office Communications Server 2007 R2 集區中移除。 **OCSUmUtil** 位於下列資料夾：

%Program Files%\\Common Files\\ Lync Server 2013\\Support\\OcsUMUtil.exe

用於執行 **OCSUmUtil** 的使用者帳戶必須具備：

  - RTCUniversalServerAdmins 與 RTCUniversalUserAdmins 群組的成員資格 (包括讀取 Exchange Server Unified Messaging 設定的權限)

  - 在指定之組織單位 (OU) 容器中建立連絡人物件的網域權限。

如需有關使用 **Get-CsExumContact** Cmdlet 的詳細資訊，請參閱 Lync Server 管理命令介面文件中的 [Get-CsExUmContact](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsExUmContact)。

