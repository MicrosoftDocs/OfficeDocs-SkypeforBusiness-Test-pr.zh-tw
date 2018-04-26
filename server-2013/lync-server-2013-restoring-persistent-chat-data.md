---
title: 還原常設聊天室資料
TOCTitle: 還原常設聊天室資料
ms:assetid: c251a7fa-50da-434b-b39a-17f5978ce736
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945649(v=OCS.15)
ms:contentKeyID: 52056217
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 還原常設聊天室資料

 

_**上次修改主題的時間：** 2013-02-18_

常設聊天室的聊天室內容會儲存在 常設聊天室資料庫 (mgc.mdf) 中。這是重要商業資料，應定期備份。除了聊天室內容，常設聊天室資料庫也會儲存有關主體 (例如使用者和群組) 的資訊，以及角色和他們在聊天室所進行的內容等存取。

如何還原常設聊天室資料取決於所使用的備份方法。

  - 如果您使用的是 SQL Server 備份程序，則必須使用 SQL Server 還原程序。

  - 如果您使用 **Export-CsPersistentChatData** Cmdlet 備份常設聊天室資料，則必須使用 **Import-CsPersistentChatData** Cmdlet 來還原資料。

