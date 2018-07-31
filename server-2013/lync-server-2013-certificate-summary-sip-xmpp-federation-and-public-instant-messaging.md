---
title: 憑證摘要 - SIP、XMPP 同盟和公用立即訊息
TOCTitle: 憑證摘要 - SIP、XMPP 同盟和公用立即訊息
ms:assetid: 933d6351-cfa6-4432-b3ed-1aff3ac92065
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ618372(v=OCS.15)
ms:contentKeyID: 49291684
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 憑證摘要 - SIP、XMPP 同盟和公用立即訊息

 

_**上次修改主題的時間：** 2015-03-09_

與 Microsoft Lync Server 2013、Lync Server 2010 及 Office Communications Server 進行同盟所需使用的憑證，通常是利用您設定、要求及指派給 Edge Server 的憑證來達成。

啟用與建立與可延伸傳訊和顯示狀態通訊協定 (XMPP) 合作夥伴的的憑證要求需要為您的 XMPP 網域增加項目。包含在憑證作為主體替代名稱 (SAN) 的記錄會是可以參與 XMPP 通訊的網域。如果您想要對整個網域啟用 XMPP，則網域可以是根層級網域 (例如，contoso.com)，或如果您想要對使用者子集啟用 XMPP，可以是選取的子網域 (例如，corp.contoso.com、finance.contoso.com)。

若要設定公用立即訊息連線的憑證，您應留意除了 America Online (AOL) 需要憑證也包含用戶端 EKU (若為 Edge 集區 時，則需要多個憑證) 之外，與其他 SIP 同盟類型，甚至與標準 Edge Server 憑證均無不同。用戶端 EKU 是憑證的附加部分，並且是指派給 Edge Server 之外部公用憑證的一部分。

若要確認您已符合 Edge Server 部署所需的正確憑證需求，請檢閱＜**請參閱**＞一節中所列的主題。



<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>元件</th>
<th>主體名稱</th>
<th>主體替代名稱 (SAN)</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>外部/Access Edge</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>sip.contoso.com</p>
<p>webcon.contoso.com</p>
<p>contoso.com</p>
<div class="alert">

> [!NOTE]  
> 支援 contoso.com XMPP 命名空間


</div>
<p>sip.fabrikam.com</p>
<div class="alert">

> [!NOTE]  
> 支援 fabrikam.com SIP 命名空間


</div>
<p>fabrikam.com</p>
<div class="alert">

> [!NOTE]  
> 支援 fabrikam.com XMPP 命名空間


</div></td>
<td><p>若要部署與 AOL 的公用 IM 連線，憑證必須來自公用 CA，且必須具有伺服器 EKU 和用戶端 EKU。憑證會指派給下列項目的外部 Edge Server 介面：</p>
<ul>
<li><p>Access Edge Service</p></li>
<li><p>Web Conferencing Edge Service</p></li>
<li><p>A/V Edge 服務</p></li>
</ul>
<div class="alert">

> [!NOTE]  
> 技術上來說，憑證並不會指派給 A/V Edge。安全通訊和驗證是採用媒體轉送驗證服務 (MRAS) 方式管理。MRAS 會使用指派給 Edge Server 內部介面的憑證。


</div>
<p>請注意，SAN 會自動根據您在拓撲產生器所下的定義新增到憑證。您可視需要為其他必須支援的 SIP 網域及其他項目新增 SAN 項目。主體名稱會複寫到 SAN 中，必須要出現才會正確運作。</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 工作

[Lync Server 2013 中的範例 XMPP 設定 – XMPP 與 Google Talk 的同盟](lync-server-2013-example-xmpp-configuration-–-xmpp-federation-with-google-talk.md)  

#### 概念

[在 Lync Server 2013 中規劃 Edge Server 憑證](lync-server-2013-plan-for-edge-server-certificates.md)  
[Lync Server 2013 中的憑證摘要 - 單一合併 Edge (使用 NAT 透過私人 IP 位址)](lync-server-2013-certificate-summary-single-consolidated-edge-with-private-ip-addresses-using-nat.md)  
[Lync Server 2013 中的憑證摘要 - 含公用 IP 位址的單一合併 Edge](lync-server-2013-certificate-summary-single-consolidated-edge-with-public-ip-addresses.md)  
[Lync Server 2013 中的憑證摘要 - 調整式合併 Edge (使用 NAT 透過私人 IP 位址進行 DNS 負載平衡)](lync-server-2013-certificate-summary-scaled-consolidated-edge-dns-load-balancing-with-private-ip-addresses-using-nat.md)  
[Lync Server 2013 中的憑證摘要 - 調整式合併 Edge (利用公用 IP 位址進行 DNS 負載平衡)](lync-server-2013-certificate-summary-scaled-consolidated-edge-dns-load-balancing-with-public-ip-addresses.md)  
[Lync Server 2013 中的憑證摘要 - 調整式合併 Edge (利用硬體負載平衡器)](lync-server-2013-certificate-summary-scaled-consolidated-edge-with-hardware-load-balancers.md)

