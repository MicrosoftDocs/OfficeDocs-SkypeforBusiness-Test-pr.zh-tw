---
title: Lync Server 2013：啟用常設聊天室伺服器原則
TOCTitle: 啟用常設聊天室伺服器原則
ms:assetid: 87063d6c-2e38-4970-b76d-2aa15f0de29e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205056(v=OCS.15)
ms:contentKeyID: 49291561
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中啟用常設聊天室伺服器原則

 

_**上次修改主題的時間：** 2012-10-06_

在 Lync Server 2013 控制台中，您可以使用 \[ 常設聊天室\] 群組的 \[ 常設聊天室原則\] 頁面管理全域、網站或使用者層級的原則，包括設定預設全域原則，以及建立其他一或多個使用者和網站原則用於您的部門。如果原則針對 常設聊天室伺服器 啟用使用者，則 常設聊天室伺服器 環境才會出現在 Lync 2013用戶端中。

> [!NOTE]  
> 在拓撲中， 常設聊天室伺服器 網站原則將全域、依使用者的集區、依使用者的網站或依使用者套用。



部署 常設聊天室伺服器 時會自動建立全域原則，此只可設定而不能刪除。由於全域原則會套用至所有使用者，所以不需要為每個使用者個別設定。

您可以建立及設定多項網站和使用者原則，當這些原則與全域原則搭配使用時，可以讓使用者使用 常設聊天室伺服器。集區和網站 常設聊天室伺服器 原則優先於全域 常設聊天室伺服器 原則，但僅限於該網站的使用者。對於獲指派指使用原則的使用者，使用者原則會優先於其全域、集區和網站原則。

> [!NOTE]  
> 若要設定和使用 常設聊天室伺服器，必須先使用 拓撲產生器將 常設聊天室伺服器 支援新增至拓撲，然後發布該拓撲。如需詳細資訊，請參閱部署文件中的＜ <a href="lync-server-2013-adding-persistent-chat-server-to-your-deployment.md">在 Lync Server 2013 中將常設聊天室伺服器新增至您的部署</a>＞。



## 本節內容

  - [在 Lync Server 2013 中設定常設聊天室的全域原則](lync-server-2013-configure-the-global-policy-for-persistent-chat.md)

  - [在 Lync Server 2013 中建立常設聊天室的網站原則](lync-server-2013-create-a-site-policy-for-persistent-chat.md)

  - [在 Lync Server 2013 中建立常設聊天室的使用者原則](lync-server-2013-create-a-user-policy-for-persistent-chat.md)

  - [在 Lync Server 2013 中將常設聊天室原則套用至使用者或使用者群組](lync-server-2013-apply-a-persistent-chat-policy-to-a-user-or-user-group.md)

