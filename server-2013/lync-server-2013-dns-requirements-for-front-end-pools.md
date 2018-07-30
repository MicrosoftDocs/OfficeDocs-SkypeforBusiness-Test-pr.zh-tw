---
title: 前端集區的 DNS 需求
TOCTitle: 前端集區的 DNS 需求
ms:assetid: ba28919c-fbbe-4c54-8bf9-2b0cd3fa39c7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412910(v=OCS.15)
ms:contentKeyID: 49292125
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 前端集區的 DNS 需求

 

_**上次修改主題的時間：** 2015-03-09_

本節描述部署前端集區所需的網域名稱系統 (DNS) 記錄。

## 前端集區的 DNS 記錄

下表指定 Lync Server 2013 前端集區部署的 DNS 需求。

### 前端集區的 DNS 需求

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>部署案例</th>
<th>DNS 需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>包含多部前端伺服器和硬體負載平衡器的前端集區 (無論 DNS 負載平衡是否也在該集區上部署)</p></td>
<td><p>同時使用 DNS 負載平衡和硬體負載平衡器時，您需要主機 (A) 記錄。針對 DNS 負載平衡建立內部 A 記錄，解析前端集區的完整網域名稱 (FQDN)。將內部 Web 服務的內部主機 (A) 記錄建立至負載平衡器的虛擬 IP (VIP) 位址。您必須使用拓撲產生器中所定義的內部 Web 服務名稱。</p>
<p>例如，如果同時使用 DNS 負載平衡和硬體負載平衡器，您在 DNS 負載平衡集區中的每一部前端伺服器會有一筆 A 記錄，以及指向硬體負載平衡器虛擬 IP 的內部 Web 服務 A 記錄：</p>
<ul>
<li><p>DNS 負載平衡：Pool01.contoso.net   IP Address of pool   10.10.10.5</p>
<div class="alert">
> [!WARNING]
> 每部前端伺服器也會有另一筆 A 記錄：

</div>
<ol>
<li><p>FE01.contoso.net    10.10.10.1</p></li>
<li><p>FE02.contoso.net    10.10.10.2</p></li>
<li><p>FE03.contoso.net    10.10.10.3</p></li>
<li><p>FE04.contoso.net    10.10.10.4</p></li>
</ol></li>
<li><p>硬體負載平衡：WebInternal.contoso.net   IP Address of HLB VIP   192.168.10.5</p></li>
</ul>
<p>除了 HTTP/HTTPS 流量，所有的流量均使用 Pool01.contoso.net record。HTTP/HTTPS 流量會使用定義的內部 Web 服務位址 (192.168.10.5)</p></td>
</tr>
<tr class="even">
<td><p>已部署 DNS 負載平衡的前端集區</p></td>
<td><p>將集區的 FQDN 解析為集區中每部伺服器之 IP 位址的一組內部 A 記錄。集區中的每部伺服器必須有一個 A 記錄。</p></td>
</tr>
<tr class="odd">
<td><p>已部署 DNS 負載平衡的前端集區</p></td>
<td><p>將集區中每部伺服器的 FQDN 解析為該伺服器之 IP 位址的一組內部 A 記錄。如需詳細資訊，請參閱規劃文件中的 <a href="lync-server-2013-dns-load-balancing.md">Lync Server 2013 中的 DNS 負載平衡</a>。</p></td>
</tr>
<tr class="even">
<td><p>具有單一前端伺服器以及專屬後端資料庫的前端集區 (但不含負載平衡器)</p></td>
<td><p>將前端集區的 FQDN 解析為單一 Enterprise Edition 前端伺服器之 IP 位址的內部 A 記錄。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>自動用戶端登入</p></td>
<td><p>針對每個受支援的 SIP 網域，對應至前端集區之 FQDN 的 _sipinternaltls._tcp.&lt;網域&gt; (透過連接埠 5061) SRV 記錄可用來驗證並重新導向用戶端登入要求。如需詳細資訊，請參閱<a href="lync-server-2013-dns-requirements-for-automatic-client-sign-in.md">Lync Server 2013 中的自動用戶端登入的 DNS 需求</a>。</p></td>
</tr>
<tr class="even">
<td><p>整合通訊 (UC) 裝置的裝置更新 Web 服務探索</p></td>
<td><p>名稱為 ucupdates-r2.&lt;SIP 網域&gt; 的內部 A 記錄，解析為裝載裝置更新 Web 服務之前端集區的 IP 位址。在 UC 裝置已開啟，但從未有使用者登入裝置的情況下，A 記錄會允許裝置探索裝載裝置更新 Web 服務的前端集區，並取得更新。否則，裝置會透過使用者首次登入時的頻內佈建取得此資訊。</p>
<div class="alert">
> [!IMPORTANT]  
> 如果您已在 Lync Server 2010 中部署裝置更新 Web 服務，表示您已建立一筆名稱為 ucupdates.<em>&lt;SIP 網域&gt;</em> 的內部 A 記錄。針對 Microsoft Office Communications Server 2007 R2，您必須另外建立一筆名稱為 ucupdates-r2.<em>&lt;SIP 網域&gt;</em> 的 DNS A 記錄。


</div></td>
</tr>
<tr class="odd">
<td><p>支援 HTTP 流量的反向 Proxy</p></td>
<td><p>一筆外部 A 記錄，將外部 Web 伺服陣列 FQDN 解析為反向 Proxy 的外部 IP 位址。 用戶端和 UC 裝置會使用這個記錄來連線至反向 Proxy。如需詳細資訊，請參閱規劃文件中的<a href="lync-server-2013-determine-dns-requirements.md">針對 Lync Server 2013 判定 DNS 需求</a>。</p></td>
</tr>
</tbody>
</table>


下表說明內部 Web 伺服陣列 FQDN 的所需 DNS 記錄範例。

### 內部 Web 伺服陣列 FQDN 的 DNS 記錄範例

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>內部 Web 伺服陣列 FQDN</th>
<th>集區 FQDN</th>
<th>DNS A 記錄</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>webcon.contoso.com</p></td>
<td><p>ee-pool.contoso.com</p></td>
<td><p>ee-pool.contoso.com 的 DNS A 記錄，解析為前端伺服器所用負載平衡器的 VIP 位址。</p>
<p>webcon.contoso.com 的 DNS A 記錄，解析為前端伺服器所用負載平衡器的 VIP 位址。</p></td>
</tr>
<tr class="even">
<td><p>ee-pool.contoso.com</p></td>
<td><p>ee-pool.contoso.com</p></td>
<td><p>ee-pool.contoso.com 的 DNS A 記錄，解析為前端集區中 Enterprise Edition 前端伺服器所用負載平衡器的虛擬 IP (VIP) 位址。</p>
<p>請注意，如果您要在此集區上使用 DNS 負載平衡，您的前端集區和內部 Web 伺服陣列不能有相同的 FQDN。</p></td>
</tr>
</tbody>
</table>

