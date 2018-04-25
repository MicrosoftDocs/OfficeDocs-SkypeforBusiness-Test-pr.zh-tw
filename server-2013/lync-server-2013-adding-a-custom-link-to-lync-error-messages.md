---
title: Lync Server 2013：新增自訂連結到 Lync 錯誤訊息
TOCTitle: 新增自訂連結到 Lync 錯誤訊息
ms:assetid: de756088-fcc3-4e47-bde8-4fa4cc852fd1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398979(v=OCS.15)
ms:contentKeyID: 52056241
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中新增自訂連結到 Lync 錯誤訊息

 

_**上次修改主題的時間：** 2013-02-20_

您可以新增連至您自己的疑難排解或服務台資訊的連結，自訂 Lync 2013 錯誤訊息。若要這樣做，請使用 **New-CSClientPolicy** 或 **Set-CSClientPolicy** Lync Server 管理命令介面 搭配 CustomLinkInErrorMessages 參數。自訂連結的文字為「按一下這裡向系統管理員取得支援主題」，而且無法自訂。

例如，下列命令會造成自訂連結出現在每個 Lync 2013 錯誤訊息的註腳區，並且將連結的目的地設定為 http://contoso.com/help/LyncHelpDesk.aspx：

    New-CsClientPolicy -Identity LyncErrorLink -CustomLinkInErrorMessages "http://contoso/help/LyncHelpDesk.aspx"

使用 **Grant-CSClientPolicy** 將此新原則指派給使用者。如需詳細資訊，請參閱 Lync Server 管理命令介面 說明文件的 **New-CSClientPolicy** 和 **Grant-CSClientPolicy**。

