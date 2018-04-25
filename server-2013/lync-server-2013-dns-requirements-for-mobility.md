---
title: 行動的 DNS 需求
TOCTitle: 行動的 DNS 需求
ms:assetid: df6962bc-2a16-440e-a333-022ebd14f957
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690040(v=OCS.15)
ms:contentKeyID: 49292556
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 行動的 DNS 需求

 

_**上次修改主題的時間：** 2015-03-09_

當您部署 Lync Server 2013 行動功能時，您可以使用 Microsoft Lync Server 2013 自動探索服務所提供的新 URL，或使用現有的 Web 服務 URL。如果使用現有的 URL，使用者需要在其行動裝置設定中手動輸入 URL。這個選項通常用於進行疑難排解。當您使用新的 URL 時，行動用戶端會自動探索 Lync Server 2013 資源。如果您支援自動探索，則需要新增網域名稱系統 (DNS) 記錄。本節說明自動探索所需的 DNS 記錄。

若要支援自動探索，您需要為每個 SIP 網域建立下列 DNS 記錄：

  - 內部 DNS 記錄，以支援從組織網路內部連線的行動使用者

  - 外部 (或公用) DNS 記錄，以支援從網際網路連線的行動使用者

內部自動探索 URL 不可從網路外部定址，而外部自動探索 URL 不可從網路內部定址。但是，如果您無法符合外部 URL 的需求，並不會影響行動用戶端功能。

DNS 記錄可以是 CNAME 記錄或 A (主機) 記錄。

**內部 DNS 記錄**

您必須建立下列其中一個內部 DNS 記錄：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>記錄類型</th>
<th>主機名稱或 SRV 定義</th>
<th>解析為</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CNAME</p></td>
<td><p>lyncdiscoverinternal.<em>&lt;sipdomain&gt;</em></p></td>
<td><p>如果您有 Director，則為 Director 集區的內部 Web 服務完整網域名稱 (FQDN)；如果您沒有 Director，則為前端集區的內部 Web 服務完整網域名稱 (FQDN)</p></td>
</tr>
<tr class="even">
<td><p>A (主機)</p></td>
<td><p>lyncdiscoverinternal.<em>&lt;sipdomain&gt;</em></p></td>
<td><p>如果您有 Director，則為 Director 集區的內部 Web 服務 IP 位址 (如果使用負載平衡器，則為虛擬 IP (VIP) 位址)；如果您沒有 Director，則為前端集區的內部 Web 服務 IP 位址</p></td>
</tr>
</tbody>
</table>


**外部 DNS 記錄**

您必須建立下列其中一個外部 DNS 記錄：


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
<td><p>lyncdiscover. <em>&lt;sipdomain&gt;</em></p></td>
<td><p>如果您有 Director，則為 Director 集區 的外部 Web 服務 FQDN；如果您沒有 Director，則為前端集區的外部 Web 服務 FQDN</p></td>
</tr>
<tr class="even">
<td><p>A (主機)</p></td>
<td><p>lyncdiscover. <em>&lt;sipdomain&gt;</em></p></td>
<td><p>反向 Proxy 的外部或公用 IP 位址 (如果使用負載平衡器，則為 VIP 位址)</p></td>
</tr>
<tr class="odd">
<td><p>SRV</p></td>
<td><p>_sipfederationtls._tcp. <em>&lt;SIP 網域&gt;</em></p>
<p>解析為 Access Edge Service 的主機 (A 或 AAAA) 記錄</p></td>
<td><p>若要支援推播通知服務與 Apple 推播通知服務，您要為包含 Microsoft Lync Mobile 用戶端的每個 SIP 網域建立一筆 SRV 記錄。</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此需求只適用於 Apple 或 Microsoft 行動裝置的 Microsoft Lync Mobile 用戶端。Andriod 與 Nokia Symbian 裝置不使用推播通知。</td>
</tr>
</tbody>
</table>

</div></td>
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
<td>Lyncdiscover 又稱為自動探索，其流量是通過反向 Proxy 傳輸。SRV 記錄會指向憑藉 Access Edge Service 解析的記錄。</td>
</tr>
</tbody>
</table>

