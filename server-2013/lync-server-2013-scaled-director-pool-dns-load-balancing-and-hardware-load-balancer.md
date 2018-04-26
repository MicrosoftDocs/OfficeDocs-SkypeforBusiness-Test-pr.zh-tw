---
title: Lync Server 2013：調整式 Director 集區 - DNS 負載平衡與硬體負載平衡器
TOCTitle: 調整式 Director 集區 - DNS 負載平衡與硬體負載平衡器
ms:assetid: a1f6ffc0-9e6e-4217-a923-025c9679e154
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205142(v=OCS.15)
ms:contentKeyID: 49291850
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的調整式 Director 集區 - DNS 負載平衡與硬體負載平衡器

 

_**上次修改主題的時間：** 2012-10-22_

經過調整的 Director 集區 (其中部署了一個以上的 Director 來處理額外容量及提供高可用性) 必須達到負載平衡，才能將用戶端與伺服器通訊分散至集區的所有成員。 Director 主控 Web 服務的方式與 前端集區極為相似。若要提供負載平衡，您可以使用硬體負載平衡或搭配使用網域名稱系統 (DNS) 負載平衡與硬體負載平衡。Web 服務需要硬體負載平衡，而 DNS 負載平衡則無法單獨提供 Web 服務所需的功能。

下列主題描述搭配使用 DNS 負載平衡與硬體負載平衡來部署 Director 集區時的規劃考量。如果您打算對 Director 集區使用硬體負載平衡，但不使用 DNS 負載平衡，請參閱＜ [Lync Server 2013 中的調整式 Director 集區 - 硬體負載平衡器](lync-server-2013-scaled-director-pool-hardware-load-balancer.md)＞以了解該拓撲的規劃需求。

![調整式 Director 集區](images/JJ205142.35a78a7a-b781-4c8f-951e-168451ba6a65(OCS.15).jpg "調整式 Director 集區")

## 本章節內容

  - [Lync Server 2013 中的憑證摘要 - DNS 與 HLB 負載平衡](lync-server-2013-certificate-summary-dns-and-hlb-load-balanced.md)

  - [Lync Server 2013 中的連接埠摘要 - DNS 與 HLB 負載平衡](lync-server-2013-port-summary-dns-and-hlb-load-balanced.md)

  - [Lync Server 2013 中的 DNS 摘要 - DNS 與 HLB 負載平衡](lync-server-2013-dns-summary-dns-and-hlb-load-balanced.md)

