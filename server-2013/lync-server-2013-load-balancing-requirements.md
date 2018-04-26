---
title: Lync Server 2013 中的負載平衡需求
TOCTitle: Lync Server 2013 中的負載平衡需求
ms:assetid: 84489328-64a4-486c-9384-a3e5c8ed9c8b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615011(v=OCS.15)
ms:contentKeyID: 49291527
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的負載平衡需求

 

_**上次修改主題的時間：** 2012-10-05_

如果您有 前端集區、Director 集區或Edge Server 集區，就需要為這些集區部署負載平衡功能。負載平衡功能會分散集區中伺服器的流量。

Lync Server 2013 支援用戶端到伺服器流量的兩種負載平衡解決方案：網域名稱系統 (DNS) 負載平衡，以及硬體負載平衡。DNS 負載平衡提供多項優點，包括簡化管理、更有效率的疑難排解，以及將大部分的 Lync Server 流量與任何潛在的硬體負載平衡器問題隔離。

決定哪一種負載平衡解決方案適合您部署中的各個集區，並記住下列限制：

  - 內部 Edge 介面和外部 Edge 介面必須使用相同類型的負載平衡。您不能在一個介面上使用 DNS 負載平衡，而在另一個介面上使用硬體負載平衡。

  - 有些類型的流量需要硬體負載平衡器。例如，HTTP 流量需要硬體負載平衡器，而非 DNS 負載平衡。DNS 負載平衡不適用於用戶端對伺服器 Web 流量。

如需關於選擇硬體負載平衡器解決方案的詳細資訊，請參閱＜[Lync Server 2013 的硬體負載平衡器需求](lync-server-2013-hardware-load-balancer-requirements.md)＞。

如果您選擇為集區使用 DNS 負載平衡，但仍需要針對某些類型的流量 (如 HTTP 流量) 實作硬體負載平衡器，硬體負載平衡器的系統管理作業已大幅簡化。如需詳細資訊，請參閱＜[Lync Server 2013 中的 DNS 負載平衡](lync-server-2013-dns-load-balancing.md)＞。

對於伺服器到伺服器流量，Lync Server 2013 使用拓撲感知負載平衡。伺服器會讀取中央管理存放區中發行的拓撲，取得拓撲中的伺服器 FQDN，並且在伺服器之間自動散佈流量。系統管理員不需要設定或管理這類負載平衡。

如果您使用 DNS 負載平衡，而且需要封鎖對於特定電腦的流量，只從集區 FQDN 移除 IP 位址並不足以達到封鎖目的，您還必須一併移除電腦的 DNS 項目。

