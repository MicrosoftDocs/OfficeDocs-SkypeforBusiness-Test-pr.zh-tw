---
title: Lync Server 2013：調整式合併 Edge (透過公用 IP 位址進行 DNS 負載平衡)
TOCTitle: 調整式合併 Edge (透過公用 IP 位址進行 DNS 負載平衡)
ms:assetid: 2b854f6d-3d3f-4961-a5f8-a03f47740df0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204761(v=OCS.15)
ms:contentKeyID: 49290420
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的調整式合併 Edge (透過公用 IP 位址進行 DNS 負載平衡)

 

_**上次修改主題的時間：** 2012-09-08_

在 Edge Server 集區拓撲中，會將兩個以上的 Edge Server 部署為資料中心之周邊網路中的負載平衡集區。網域名稱系統 (DNS) 負載平衡會用於外部和內部 Edge 介面的流量。

如果您的組織需要支援超過 15,000 個 Access Edge 服務用戶端連線、1,000 個作用中的 Lync Server Web 會議服務用戶端連線，或 500 個同時 A/V Edge 工作階段，且/或 Edge Server 的高可用性相當重要，此拓撲提供了擴充性和容錯移轉支援的優點。

下圖未顯示 Director，以及 Edge Server 與 前端集區或伺服器之間內部網路所部署的選用伺服器角色。如需 Director 拓撲的詳細資訊，請參閱＜ [Lync Server 2013 中 Director 的必要元件](lync-server-2013-components-required-for-the-director.md)＞。此圖代表一個反向 Proxy 伺服器。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此圖提供方向與 IP 位址指定範例之參考，不代表目前正確傳入與傳出流量的實際通訊流程。此圖顯示詳細的可能流量。有關傳入 (聆聽連接埠) 與傳出 (目的地伺服器或用戶端) 的流量流程資訊，各案例的連接埠摘要圖表均有詳細說明。例如從通訊協定 (TCP) 角度來看，TCP 443 其實僅供連入 (Edge 或反向 Proxy)，只是雙向流量流程。此外，此圖顯示網路位址轉譯 (NAT) 發生時 (連入的目的地位址改變，連出的來源位址改變)，流量改變的特性。外部/內部防火牆與伺服器介面的範例僅供參考。最後顯示的是預設閘道器與路由器之關聯性範例 (若適用)。另外請注意，圖表使用 <em>.com</em> DNS 區域代表反向 Proxy 與 Edge Server 的外部 DNS 區域， <em>.net</em> DNS 區域則代表內部 DNS 區域。</td>
</tr>
</tbody>
</table>


Microsoft Lync Server 2013 的新功能支援 IPv6 定址。指定方法與 IPv4 定址類似，IPv6 位址必須是指定 IPv6 位址空間的一部分。本主題的位址僅為範例。您取得的 IPv6 位址，必須要能在部署中作用，提供正確的範圍，並與內部/外部定址交互操作。 Windows Server 提供的某項功能，對轉換 IPv6 操作，以及 IPv4 與 IPv6 通訊 (稱為「 *雙重堆疊* 」至關重要。雙重堆疊是 IPv4 與 IPv6 各別的網路堆疊。雙重堆疊可讓您同時指派 IPv4 與 IPv6 位址，且讓伺服器根據其他主機與用戶端的需求互相通訊。

您要用於 IPv6 定位的一般位址類型是 IPv6 全域位址 (類似公開的 IPv4 位址)、IPv6 唯一本機位址 (類似私人 IPv4 位址範圍) 與 IPv6 連結本機位址 (類似 Windows Server 的 IPv4 自動私人 IP 位址)

現有的 IPv6 網路位址轉譯技術 (NAT) 支援 NAT IPv6 to IPv4 (通稱為 NAT64) 與 NAT IPv6 to IPv6 (通稱為 NAT66)。現有的 NAT 技術代表 Lync ServerEdge Server 的五個案例仍然有效。

<table>
<thead>
<tr class="header">
<th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>IPv6 是一個複雜的主題，必須與網路小組和網際網路供應商詳細規劃，確保指定的位址符合 Windows 伺服器層級及 Lync Server 2013 層級要求，也可如預期般運作。如需 IPv6 定址與規劃的其他資源，請參閱本主題最下方的連結。</td>
</tr>
</tbody>
</table>


![調整式合併 Edge 拓撲](images/JJ204761.7c1e3e6b-9b1b-4ac6-b0e7-9c256dbc2537(OCS.15).jpg "調整式合併 Edge 拓撲")

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若使用通話許可控制 (Call Admission Control, CAC)，您仍必須指派 IPv4 位址到 Edge Server 內部介面。CAC 使用 IPv4 位址，且必須開放 IPv4 位址以供操作。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [Lync Server 2013 中的憑證摘要 - 調整式合併 Edge (利用公用 IP 位址進行 DNS 負載平衡)](lync-server-2013-certificate-summary-scaled-consolidated-edge-dns-load-balancing-with-public-ip-addresses.md)

  - [Lync Server 2013 中的連接埠摘要 - 調整式合併 Edge (利用公用 IP 位址進行 DNS 負載平衡)](lync-server-2013-port-summary-scaled-consolidated-edge-dns-load-balancing-with-public-ip-addresses.md)

  - [Lync Server 2013 中的 DNS 摘要 - 調整式合併 Edge (透過公用 IP 位址進行 DNS 負載平衡)](lync-server-2013-dns-summary-scaled-consolidated-edge-dns-load-balancing-with-public-ip-addresses.md)

## 請參閱

#### 其他資源

[IP 版本 6 定址結構](http://tools.ietf.org/html/rfc4291)  
[IPv6 全域單點傳播位址格式](http://tools.ietf.org/html/rfc3587)  
[唯一本機 IPv6 單一位址](http://tools.ietf.org/html/rfc4193)

