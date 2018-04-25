---
title: 移轉多個網站與集區
TOCTitle: 移轉多個網站與集區
ms:assetid: a6d726d2-564d-4b39-a97c-5656a673292a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205165(v=OCS.15)
ms:contentKeyID: 49291916
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉多個網站與集區

 

_**上次修改主題的時間：** 2012-09-17_

Lync Server 2013 支援多網站和多集區部署。將多個集區從 Lync Server 2010 移轉至 Lync Server 2013 的程序需要下列考量：

1.  部署 Lync Server 2013 試驗集區之後，您必須定義一小組將移至 Lync Server 2013 集區的試驗使用者，以及用於驗證使用者功能的方法。例如，將使用者移至試驗集區之後，驗證使用者的會議原則是否已移至 Lync Server 2013。

2.  在試驗集區中部署 Edge Server 之後，您必須驗證外部使用者是否可與 Lync Server 2013 集區通訊。

3.  將同盟路由從 Lync Server 2010 Edge Server 轉換至試驗 Lync Server 2013 Edge Server 之後，您必須驗證同盟使用者是否可與 Lync Server 2013 集區通訊。

4.  移動所有使用者與非使用者的連絡人物件之後，必須驗證 Lync Server 2010 集區是否為空。

5.  確定 Lync Server 2010 集區為空之後，即可停用該集區。
    
    如需如何停用舊版 Lync Server 2010 集區及伺服器的詳細資訊，請參閱＜ [第 8 階段：解除委任舊版集區](phase-8-decommission-legacy-pools.md)＞。

