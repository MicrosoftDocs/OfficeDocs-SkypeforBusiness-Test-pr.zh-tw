---
title: Lync Server 2013：使用拓撲產生器設定高可用性和災害復原
TOCTitle: 使用拓撲產生器設定高可用性和災害復原
ms:assetid: abc1a25d-1f5e-46ef-91d2-0144fc847206
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205172(v=OCS.15)
ms:contentKeyID: 49291961
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中使用拓撲產生器設定高可用性和災害復原

 

_**上次修改主題的時間：** 2012-10-06_

在 拓撲產生器中執行下列步驟，以設定 常設聊天室伺服器 的高可用性與災害復原。

1.  新增鏡像資料庫與 Log Shipping 次要資料庫 SQL Server 存放區。

2.  編輯 常設聊天室伺服器 服務屬性：
    
    1.  啟用主要資料庫的鏡像。
    
    2.  新增主要鏡像 SQL Server 存放區。
    
    3.  啟用 SQL Server Log Shipping 資料庫。
    
    4.  新增 SQL Server Log Shipping 次要 SQL Server 存放區。
    
    5.  新增次要資料庫的 SQL Server 存放區鏡像。
    
    6.  發行拓撲。

