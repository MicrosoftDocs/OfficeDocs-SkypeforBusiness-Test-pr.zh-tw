---
title: Lync Server 2013：將 Survivable Branch Appliance 連接到 Lync Server 2013 前端集區
TOCTitle: 將 Survivable Branch Appliance 連接到 Lync Server 2013 前端集區
ms:assetid: 3c7ca33f-5295-4d82-9152-41d8bc6f35cf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688026(v=OCS.15)
ms:contentKeyID: 49890027
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將 Survivable Branch Appliance 連接到 Lync Server 2013 前端集區

 

_**上次修改主題的時間：** 2012-10-05_

每一個 Survivable Branch Appliance (SBA) 都與一個 前端集區關聯，作為 SBA 的備份登錄器。當 前端集區升級至 Lync Server 2013 時，SBA 必須在 前端集區升級時，解除與 前端集區的關聯。 前端集區升級之後，SBA 可以再與 前端集區重新關聯。這牽涉到在拓撲產生器中從拓撲刪除 SBA，然後再新增 SBA 到拓撲產生器。在從拓撲移除 SBA 之前，必須將位於 SBA 的使用者移至其他 前端集區。將 SBA 新增回拓撲之後，可以再將使用者移回 SBA。

這些步驟的摘要如下：

1.  將位於 SBA 的分支使用者移至其他 前端集區。

2.  將 SBA 從拓撲中移除，解除現有作為備份登錄器的 前端集區關聯。

3.  將 前端集區升級至 Microsoft Lync Server 2013。

4.  將 SBA 新增回拓撲。

5.  將 SBA 與新的 前端集區關聯，作為備份登錄器。

6.  將分支使用者移回 SBA。

## 本章節內容

  - [將 Lync Server 2013 Survivable Branch Appliance 分支網站新增至您的拓撲](lync-server-2013-add-lync-server-2013-survivable-branch-appliance-branch-site-to-your-topology.md)

  - [將 Lync Server 2010 Survivable Branch Appliance 分支網站新增至您的拓撲](lync-server-2013-add-lync-server-2010-survivable-branch-appliance-branch-site-to-your-topology.md)

