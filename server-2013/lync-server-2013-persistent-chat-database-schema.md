---
title: Lync Server 2013：常設聊天室資料庫結構描述
TOCTitle: 常設聊天室資料庫結構描述
ms:assetid: 58d7d94f-42f5-4c3e-8fe5-901fbe92152e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558653(v=OCS.15)
ms:contentKeyID: 49291001
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的常設聊天室資料庫結構描述

 

_**上次修改主題的時間：** 2012-09-18_

本主題記載 Lync Server 2013  通訊軟體中的 常設聊天室資料庫結構描述。

常設聊天室資料庫是指對應至 Lync Server 2013 後端伺服器角色 **PersistentChatStore** (對應至 MGC 資料庫) 和 **PersistentChatComplianceStore** (對應至 Mgccomp 資料庫) 的資料庫。發行此結構描述的目標是讓您能夠建立查詢，並深入了解建立關於交談使用方式、作用中聊天室、前幾名的張貼者等實用報告的資訊。

> [!IMPORTANT]  
> 我們保留發展此結構描述的權利。Microsoft 不保證會維持此發行的結構描述之完整回溯相容性。



請遵循以下最佳做法：

  - 不支援 SELECT\* //，因為欄清單可以擴充。

  - 不支援使用者產生的結構描述修改。

  - 不支援寫入作業。

  - 測試您在典型大小之資料庫上建立的任何查詢，以確定查詢可以在符合您需求的層級上執行。

## 本章節內容

  - [Lync Server 2013 中的常設聊天室伺服器清單表格](lync-server-2013-list-of-persistent-chat-server-tables.md)

  - [Lync Server 2013 中常設聊天室伺服器規範表的清單](lync-server-2013-list-of-persistent-chat-server-compliance-tables.md)

  - [Lync Server 2013 中的常設聊天室伺服器表格詳細資料](lync-server-2013-persistent-chat-server-table-details.md)

  - [Lync Server 2013 的常設聊天室資料庫查詢範例](lync-server-2013-sample-persistent-chat-database-queries.md)

