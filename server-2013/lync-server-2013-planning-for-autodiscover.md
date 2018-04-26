---
title: 規劃自動探索
TOCTitle: 規劃自動探索
ms:assetid: 51f1ff94-1d64-4e6d-a878-b86fa07edc2d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945628(v=OCS.15)
ms:contentKeyID: 52056126
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 規劃自動探索

 

_**上次修改主題的時間：** 2013-02-16_

針對 Lync Server 的自動探索推出於 Lync Server 2010 累計更新 (2011 年 11 月)。此初始實作自動探索的主要目的是提供 Lync Mobile 尋找 Mobility Service (Mcx) 的方法。Lync Server 2013 中的自動探索服務現在是所有用戶端在尋找伺服器和使用者服務時所用的服務。Microsoft Lync Server 2013 自動探索服務執行於 Director 和前端伺服器上。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需自動探索以及與用戶端通訊之內容的詳細技術資訊，請參閱＜<a href="lync-server-2013-understanding-autodiscover.md">了解自動探索</a>＞。<br />
Mobility 仍為不同的案例，且 Mobility Services 還是需要某些特別的規劃。如需詳細資訊，請參閱＜<a href="lync-server-2013-planning-for-mobility.md">Lync Server 2013 中的行動規劃</a>＞。</td>
</tr>
</tbody>
</table>


當在 Lync Server 2010 中推出自動探索時必須做出妥協，才能實作這個可能需要對現有伺服器部署變更憑證的服務。自動探索可透過連接埠 TCP 443 用於 HTTPS，或透過連接埠 TCP 80 用於 HTTP。如果決定使用 HTTPS，則需要重新發行反向 Proxy、Director 及前端伺服器上的憑證，才能配合所需的 `lyncdiscover.<網域>` 和 `lyncdiscoverinternal.<網域>` DNS 記錄。如果決定使用 HTTP，則可使用 DNS CNAME (或別名) 記錄，在憑證上使用現有的名稱，即可避免重新發行憑證。使用 HTTP 也表示初始通訊是未加密的。

因為 Lync Server 2013 對所有用戶端都使用自動探索，所以主要案例是只使用 HTTPS 並且建立含 lyncdiscover.\<網域\> 的憑證，做為設定反向 Proxy、Director 及前端伺服器的一部分。如果要在 Lync Server 2010 的升級部署中實作自動探索，建議您使用 HTTP 來避免重新發行憑證。下列章節將提供這兩個案例的指引。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>外部 Web 服務發行規則所使用的憑證主體替代名稱清單，必須針對組織內的每個 SIP 網域，各包含一個 <em>lyncdiscover.&lt;SIP 網域&gt;</em> 項目。 如需 Director、前端伺服器和反向 Proxy 所需之主體替代名稱項目的詳細資訊，請參閱＜<a href="lync-server-2013-certificate-summary-autodiscover.md">憑證摘要 - 自動探索</a>＞。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [憑證摘要 - 自動探索](lync-server-2013-certificate-summary-autodiscover.md)

  - [Lync Server 2013 中的連接埠摘要 - 自動探索](lync-server-2013-port-summary-autodiscover.md)

  - [Lync Server 2013 中的 DNS 摘要 - 自動探索](lync-server-2013-dns-summary-autodiscover.md)

  - [混合與分割網域 - 自動探索](lync-server-2013-hybrid-and-split-domain-autodiscover.md)

