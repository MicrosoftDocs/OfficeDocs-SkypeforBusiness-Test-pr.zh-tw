---
title: Lync Server 2013：Director 的必要元件
TOCTitle: Director 的必要元件
ms:assetid: 15c7c8d4-b93f-4386-b2d1-d76dab8f801e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398228(v=OCS.15)
ms:contentKeyID: 49290196
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中 Director 的必要元件

 

_**上次修改主題的時間：** 2012-09-08_

建立及設定 Director 所需的唯一元件，就是部署 Director 伺服器角色。若要執行此作業，請使用 拓撲產生器，並且在 Director 集區節點中定義單一電腦集區或多電腦集區。定義 Director 或 Director 集區之後，在將要用做 Director 的電腦上執行 \[ Lync Server 部署精靈\]。在 Director 集區的案例中，您要在將做為集區成員的每部伺服器上執行 \[ Lync Server 部署精靈\]。

## 拓撲

您可以實作單一 Director 伺服器，也可以實作 Director 集區。 Director 一定是個別的伺服器或集區，不會與 Lync Server 2013 中的任何其他伺服器角色組合在一起。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果沒有部署 Director， 前端伺服器或 前端集區將會採用 Director 角色。</td>
</tr>
</tbody>
</table>


Director 集區必須負載平衡。您可以執行下列其中一項：

  - 建立拓撲，針對其他流量類型的 Web 服務和網域名稱系統 (DNS) 負載平衡，使用硬體負載平衡器。
    
    [Lync Server 2013 中的調整式 Director 集區 - DNS 負載平衡與硬體負載平衡器](lync-server-2013-scaled-director-pool-dns-load-balancing-and-hardware-load-balancer.md)

  - 建立拓撲，針對 Director 集區所需的負載平衡，使用硬體負載平衡器。
    
    [Lync Server 2013 中的調整式 Director 集區 - 硬體負載平衡器](lync-server-2013-scaled-director-pool-hardware-load-balancer.md)

