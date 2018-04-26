---
title: Lync Server 2013 中的 DNS 摘要 - 自動探索
TOCTitle: Lync Server 2013 中的 DNS 摘要 - 自動探索
ms:assetid: b336a2ae-0e58-4b74-b606-aedbbd411587
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945644(v=OCS.15)
ms:contentKeyID: 52056183
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 DNS 摘要 - 自動探索

 

_**上次修改主題的時間：** 2015-03-09_

自動探索是一種彈性的服務，可透過 HTTP 或 HTTPS 進行通訊。若要完成此動作，主控自動探索服務之伺服器所使用的網域名稱系統 (DNS) 和憑證必須正確設定。憑證需求可參閱＜[憑證摘要 - 自動探索](lync-server-2013-certificate-summary-autodiscover.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 用戶端的 DNS 查詢邏輯使用解析的特定順序。DNS 中應該一律包含 lyncdiscoverinternal.&lt;網域&gt;和 lyncdiscover.&lt;網域&gt;。排除 lyncdiscoverinternal.&lt;網域&gt;記錄將造成內部用戶端無法連線至預定服務或不正確的自動探索回應。</td>
</tr>
</tbody>
</table>


### 內部 DNS 記錄

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>記錄類型</th>
<th>主機名稱</th>
<th>解析為</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CNAME</p></td>
<td><p>Lyncdiscoverinternal.<em>&lt;內部網域名稱&gt;</em></p></td>
<td><p>Director 集區 (如果您有的話) 或前端集區 (如果您沒有 Director 的話) 的內部 Web 服務 FQDN。</p></td>
</tr>
<tr class="even">
<td><p>A (主機，對於 IPv6 則為 AAAA)</p></td>
<td><p>lyncdiscoverinternal.<em>&lt;內部網域名稱&gt;</em></p></td>
<td><p>如果您有 Director，則為 Director 集區的內部 Web 服務 IP 位址 (如果使用負載平衡器，則為虛擬 IP (VIP) 位址)；如果您沒有 Director，則為前端集區的內部 Web 服務 IP 位址。</p></td>
</tr>
</tbody>
</table>


您必須建立下列其中一個外部 DNS 記錄：

### 外部 DNS 記錄

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>記錄類型</th>
<th>主機名稱</th>
<th>解析為</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CNAME</p></td>
<td><p>lyncdiscover. <em>&lt;SIP 網域&gt;</em></p></td>
<td><p>如果您有 Director，則為 Director 集區的外部 Web 服務 FQDN；如果您沒有 Director，則為前端集區的外部 Web 服務 FQDN。</p></td>
</tr>
<tr class="even">
<td><p>A (主機，對於 IPv6 則為 AAAA)</p></td>
<td><p>lyncdiscover. <em>&lt;SIP 網域&gt;</em></p></td>
<td><p>反向 Proxy 的外部或公用 IP 位址。</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>外部流量會通過反向 Proxy。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>行動裝置用戶端不支援來自不同網域的多個安全通訊端階層 (SSL) 憑證。因此，不支援透過 HTTPS 將 CNAME 重新導向至不同的網域。例如，不支援透過 HTTPS 將 lyncdiscover.contoso.com 的 DNS CNAME 記錄重新導向至 director.contoso.net 的位址。在這樣的拓撲中，行動裝置用戶端需要使用 HTTP 來進行第一個要求，以透過 HTTP 來解析 CNAME 重新導向。後續的要求則會使用 HTTPS。若要支援此案例，您需要以連接埠 80 的 Web 發行規則來設定反向 Proxy (HTTP)。如需詳細資訊，請參閱＜<a href="lync-server-2013-configuring-the-reverse-proxy-for-mobility.md">在 Lync Server 2013 中設定行動的反向 Proxy</a>＞中的＜建立連接埠 80 的網頁發行規則＞。支援透過 HTTPS 將 CNAME 重新導向至相同網域。在此情況下，目的地網域的憑證包含來源網域。</td>
</tr>
</tbody>
</table>


## 請參閱

#### 工作

[在 Lync Server 2013 中設定行動的反向 Proxy](lync-server-2013-configuring-the-reverse-proxy-for-mobility.md)  

#### 概念

[憑證摘要 - 自動探索](lync-server-2013-certificate-summary-autodiscover.md)

