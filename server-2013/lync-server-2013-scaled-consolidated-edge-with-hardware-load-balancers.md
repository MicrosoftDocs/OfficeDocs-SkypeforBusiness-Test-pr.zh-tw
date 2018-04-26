---
title: Lync Server 2013：含硬體負載平衡器的調整式合併 Edge
TOCTitle: 含硬體負載平衡器的調整式合併 Edge
ms:assetid: 6783e225-9677-415a-8731-0bf2e2c4cf8b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398478(v=OCS.15)
ms:contentKeyID: 49291169
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中含硬體負載平衡器的調整式合併 Edge

 

_**上次修改主題的時間：** 2012-10-21_

在 Edge 集區拓撲中，會將兩個以上的 Edge Server 部署為資料中心之周邊網路中的負載平衡集區。往外部及內部 Edge Server 介面的流量會使用硬體負載平衡。

如果您的組織需要支援 15,000 個以上的 Access Edge Service 用戶端連線、1,000 個作用中 Web Conferencing Edge Service 用戶端連線或 500 個並行 A/V Edge 服務 工作階段，而且 Edge Server 的高可用性十分重要，則此拓撲提供延展性及容錯移轉支援的優點。

此圖並未顯示 Director，此為內部網路中部署於 Edge Server 和 前端集區或伺服器之間的選用伺服器角色。如需 Director 拓撲的詳細資訊，請參閱＜ [Lync Server 2013 中 Director 的必要元件](lync-server-2013-components-required-for-the-director.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此圖說明 IP 位址定址的方向和範例，但並未嘗試使用正確的傳出和傳入流量來表示實際的通訊流量。此圖表示的是可能流量的高階檢視。有關傳入 (至聆聽連接埠) 和傳出 (至目的地伺服器或用戶端) 流量的詳細資訊，會在每個案例中表示於連接埠摘要圖中。例如，TCP 443 實際上僅為傳入 (至 Edge Server 或反向 Proxy)，且從通訊協定 (TCP) 觀點來看，僅為雙向流量。另外，此圖也顯示在 NAT (網路位址轉譯) 發生之時 (目的地位址在傳入時變更，來源位址在傳出時變更) 流量在變化時的特性。外部及內部防火牆和伺服器介面範例僅顯示作為參考之用。最後，預設閘道和路由關係會視需要顯示。請同時注意，圖表使用 <em>.com</em> DNS 區域來表示反向 Proxy 和 Edge Server 的外部 DNS 區域，而 <em>.net</em> DNS 區域指的是內部 DNS 區域。</td>
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


**硬體負載平衡器設定**

如需詳細資訊，請參閱＜ [外部使用者在 Lync Server 2013 中存取時所需的元件](lync-server-2013-components-required-for-external-user-access.md)＞中的＜A/V Edge 的硬體負載平衡器需求＞一節。

**調整式合併 Edge 拓撲 (硬體負載平衡)**

![調整式合併 Edge 拓撲](images/Gg398478.3a57cd0d-8de4-4ecc-a783-4dff5b3456a2(OCS.15).jpg "調整式合併 Edge 拓撲")

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

  - [Lync Server 2013 中的憑證摘要 - 調整式合併 Edge (利用硬體負載平衡器)](lync-server-2013-certificate-summary-scaled-consolidated-edge-with-hardware-load-balancers.md)

  - [Lync Server 2013 中的連接埠摘要 - 調整式合併 Edge (利用硬體負載平衡器)](lync-server-2013-port-summary-scaled-consolidated-edge-with-hardware-load-balancers.md)

  - [Lync Server 2013 中的 DNS 摘要 - 調整式合併 Edge (利用硬體負載平衡器)](lync-server-2013-dns-summary-scaled-consolidated-edge-with-hardware-load-balancers.md)

## 請參閱

#### 其他資源

[IP 版本 6 定址結構](http://tools.ietf.org/html/rfc4291)  
[IPv6 全域單點傳播位址格式](http://tools.ietf.org/html/rfc3587)  
[唯一本機 IPv6 單一位址](http://tools.ietf.org/html/rfc4193)

