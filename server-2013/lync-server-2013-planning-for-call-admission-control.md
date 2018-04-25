---
title: Lync Server 2013：規劃通話許可控制
TOCTitle: 規劃通話許可控制 (CAC)
ms:assetid: ca367138-adf5-4119-bc40-5ddf335ed22f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398842(v=OCS.15)
ms:contentKeyID: 49292317
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中規劃通話許可控制

 

_**上次修改主題的時間：** 2012-09-21_

對於 IP 式的整合通訊 (UC) 應用程式 (例如電話語音、視訊和應用程式共用)，可用的企業網路頻寬通常不會視為 LAN 環境內的限制因素。不過，在用於將網站互連的 WAN 連結上，網路頻寬可能有限。當湧進大量的網路流量讓 WAN 連結不勘負荷時，就會使用現行機制 (例如佇列、緩衝和封包捨棄) 解決壅塞的情況。額外的流量通常會延到網路壅塞情況舒緩再傳送，或是在不得已的情況下直接被捨棄。在這種情況下，如果資料流量是傳統資料流量，則接收用戶端可以自行恢復過來。但如果資料流量是即時流量 (例如整合通訊)，就無法透過這種方式解決網路壅塞，這是因為只要有一點點的耽擱或封包遺失，整合通訊流量就會受到影響。WAN 上發生壅塞可能導致使用者獲得不好的經驗品質 (QoE)。如果是即時流量，遇到壅塞情況時最好是拒絕通話，而不要提供品質不良的連線。

通話許可控制 (CAC) 會判斷是否有足夠的網路頻寬可建立品質在可接受範圍內的即時工作階段。在 Lync Server 2013 中，CAC 只會控制音訊和視訊的即時流量，不會影響資料流量。如果預設的 WAN 路徑沒有必要的頻寬，CAC 可能會嘗試透過網際網路路徑或公用交換電話網路 (PSTN) 路由傳送通話。CAC 只在 Lync Server 中提供。

本節描述通話許可控制功能，並且解釋如何規劃 CAC。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 具有三項進階的 企業語音功能：通話許可控制 (CAC)、緊急服務 (E9-1-1) 以及媒體旁路。如需這三項功能全域的規劃資訊概觀，請參閱 <a href="lync-server-2013-network-settings-for-the-advanced-enterprise-voice-features.md">Lync Server 2013 中的進階企業語音功能的網路設定</a>。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [Lync Server 2013 中的通話許可控制概觀](lync-server-2013-overview-of-call-admission-control.md)

  - [在 Lync Server 2013 中定義通話許可控制需求](lync-server-2013-defining-your-requirements-for-call-admission-control.md)

  - [範例：在 Lync Server 2013 中收集通話許可控制服務需求](lync-server-2013-example-of-gathering-your-requirements-for-call-admission-control.md)

  - [Lync Server 2013 中 CAC 的元件與拓撲](lync-server-2013-components-and-topologies-for-cac.md)

  - [Lync Server 2013 中通話許可控制的最佳做法](lync-server-2013-best-practices-for-call-admission-control.md)

  - [Lync Server 2013 中的通話許可控制的部署檢查清單](lync-server-2013-deployment-checklist-for-call-admission-control.md)

