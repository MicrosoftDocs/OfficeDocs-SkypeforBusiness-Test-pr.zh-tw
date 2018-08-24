---
title: 設定預設圖片選項
TOCTitle: 設定預設圖片選項
ms:assetid: b1c986f0-6400-447a-9e36-78c1c3a4f793
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn205074(v=OCS.15)
ms:contentKeyID: 53901822
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定預設圖片選項

 

_**上次修改主題的時間：** 2013-03-22_

依照預設，使用者的圖片會自動顯示。如果使用者希望隱藏自己的圖片，可以在 Lync 用戶端上選取 **\[隱藏我的圖片\]** 選項。不過，一些其他 Office 應用程式會略過此設定。

如果在使用者關閉圖片顯示的情況下，由於圖片仍有可能顯示而造成使用者顧慮時，您可以於全域範圍變更 Lync 圖片顯示設定，或針對特定網站或服務變更設定，避免預設顯示使用者圖片的問題。使用下列 Lync Server 管理命令介面 cmdlet，可以避免顯示使用者的圖片，除非使用者在用戶端上明確選取 **\[顯示我的圖片\]** 選項：

    Set-CsPrivacyConfiguration -DisplayPublishedPhotoDefault $False

如需更多有關此 Cmdlet 的資訊，請參閱 Lync Server 管理命令介面 文件中的＜[Set-CsPrivacyConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsPrivacyConfiguration)＞。

