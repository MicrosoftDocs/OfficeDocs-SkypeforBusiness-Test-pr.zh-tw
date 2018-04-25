---
title: Lync Server 2013：調整式 Director 集區 - 硬體負載平衡器
TOCTitle: 調整式 Director 集區 - 硬體負載平衡器
ms:assetid: cf34759a-b384-479c-855f-ea5e80a234b6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205316(v=OCS.15)
ms:contentKeyID: 49292366
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的調整式 Director 集區 - 硬體負載平衡器

 

_**上次修改主題的時間：** 2012-09-08_

部署多個 Director 以處理額外的容量和提供高可用性的調整式 Director 集區，需要負載平衡以將用戶端與伺服器通訊分散到集區的所有成員。 Director 裝載 Web 服務的方式和 前端集區極為類似。Web 服務需要硬體負載平衡。

下列主題說明使用硬體負載平衡來部署 Director 集區 的規劃考量。如果您想讓 Director 集區使用硬體負載平衡與 DNS 負載平衡，請參閱＜ [Lync Server 2013 中的調整式 Director 集區 - DNS 負載平衡與硬體負載平衡器](lync-server-2013-scaled-director-pool-dns-load-balancing-and-hardware-load-balancer.md)＞主題，文中說明規劃那類拓撲的需求。

![調整式 Director 集區](images/JJ205316.cfa892b9-5b24-4245-b5bd-c5da21984eeb(OCS.15).jpg "調整式 Director 集區")

## 本章節內容

  - [Lync Server 2013 中的憑證摘要 - 調整式 Director 集區 (硬體負載平衡器)](lync-server-2013-certificate-summary-scaled-director-pool-hardware-load-balancer.md)

  - [Lync Server 2013 中的連接埠摘要 - 調整式 Director 集區 (硬體負載平衡器)](lync-server-2013-port-summary-scaled-director-pool-hardware-load-balancer.md)

  - [Lync Server 2013 中的 DNS 摘要 - 調整式 Director 集區 (硬體負載平衡器)](lync-server-2013-dns-summary-scaled-director-pool-hardware-load-balancer.md)

