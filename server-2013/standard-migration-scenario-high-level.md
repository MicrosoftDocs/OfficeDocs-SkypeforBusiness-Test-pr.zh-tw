---
title: 標準移轉案例 - 高層級
TOCTitle: 標準移轉案例 - 高層級
ms:assetid: e768a7ca-44e3-4969-a6d9-7ed3e7029c5c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205354(v=OCS.15)
ms:contentKeyID: 49292652
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 標準移轉案例 - 高層級

 

_**上次修改主題的時間：** 2013-01-30_

移轉 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2群組聊天到 Lync Server 2013、 常設聊天室伺服器 時，請從下列項目開始操作。標準的 Lync Server 2013 移轉路徑如下：

  - 貴公司已部署 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2群組聊天，且您想部署 Lync Server 2013、 常設聊天室伺服器。

  - 依序部署 Lync Server 2013、 Persistent Chat Server 集區。

  - 準備並規劃移轉您的 常設聊天室 會議室，並決定適當時機來關閉系統以進行移轉。

  - 執行 Windows PowerShell Cmdlet 進行移轉 (**Export-CsPersistentChatData** 與 **Import-CsPersistentChatData**)，將內容移至常設聊天室伺服器。

  - 確認移轉已成功。

  - 解除委任舊版部署。

  - 設定 常設聊天室伺服器，讓舊版用戶端可連線到 Lync Server 2013、 常設聊天室伺服器。這是必要措施，因為部署新用戶端需要一段時間，且您會想讓使用舊版用戶端的現有使用者盡快使用得到聊天室。

  - 部署新用戶端，同時持續為使用舊版 群組聊天 (用戶端) 的工作者提供協助，確保他們能使用聊天室。

