---
title: Lync Server 2013：簡單 URL 的 DNS 需求
TOCTitle: 簡單 URL 的 DNS 需求
ms:assetid: 3a3c9b22-892f-45a7-b05c-539d358a1a86
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425874(v=OCS.15)
ms:contentKeyID: 49290635
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中簡單 URL 的 DNS 需求

 

_**上次修改主題的時間：** 2015-03-09_

Lync Server 2013 支援簡單 URL，讓使用者更容易加入會議，系統管理員也更容易取得 Lync Server 系統管理工具。如需簡單 URL 的詳細資訊，請參閱＜ [在 Lync Server 2013 中規劃簡單 URL](lync-server-2013-planning-for-simple-urls.md)＞。

Lync Server 支援下列三種簡單 URL：Meet、Dial-In 和 Admin。您必須設定 Meet 和 Dial-In 的簡單 URL，而 Admin 的簡單 URL 則是選用的。需要用來支援簡單 URL 的網域名稱系統 (DNS) 記錄，視您定義這些簡單 URL 的方式而定，以及是否要支援簡單 URL 的災害復原。

## 簡單 URL 選項 1

在選項 1 中，您為每個簡單 URL 各建立一個新的基底 URL。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當使用者按一下簡單 URL 會議連結時，DNS A 記錄解析為的伺服器會判斷要啟動的正確用戶端軟體。用戶端軟體啟動後，便會自動與裝載會議的集區進行通訊。透過這個方式，無論簡單 URL DNS A 記錄是解析為哪個伺服器或集區，都會將使用者導向至包含會議內容的正確伺服器。</td>
</tr>
</tbody>
</table>


### 簡單 URL 選項 1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>簡單 URL</strong></p></td>
<td><p><strong>範例</strong></p></td>
</tr>
<tr class="even">
<td><p>會議 (Meet)</p></td>
<td><p>https://meet.contoso.com、https://meet.fabrikam.com 等等 (組織中的每個 SIP 網域各一個)</p></td>
</tr>
<tr class="odd">
<td><p>撥入</p></td>
<td><p>https://dialin.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Admin</p></td>
<td><p>https://admin.contoso.com</p></td>
</tr>
</tbody>
</table>


如果使用選項 1，您必須定義下列項目：

  - 對於每個 Meet 簡單 URL，如果您已部署 Director，則需要有一筆 DNS A 記錄，並讓其將 URL 解析為 Director 的 IP 位址。否則，即應解析為前端集區的負載平衡器的 IP 位址。如果您未部署集區，且使用 Standard Edition Server 部署，則 DNS A 記錄必須解析為組織中某部 Standard Edition Server 的 IP 位址。
    
    如果組織中有多個 SIP 網域而您使用此選項，您必須為每個 SIP 網域建立 Meet 簡單 URL，且每個 Meet 簡單 URL 各需有一筆 DNS A 記錄。例如，如果您同時有 contoso.com 和 fabrikam.com，則需為 https://meet.contoso.com 和 https://meet.fabrikam.com 各建立 DNS A 記錄。
    
    或者，如果您有多個 SIP 網域且想減少這些簡單 URL 的 DNS 記錄和憑證需求，請使用本主題稍後所述的選項 3。

  - 對於 Dial-in 簡單 URL，如果您已部署 Director，則需要有一筆 DNS A 記錄，並讓其將 URL 解析為 Director 的 IP 位址。否則，即應解析為前端集區的負載平衡器的 IP 位址。如果您未部署集區，且使用 Standard Edition Server 部署，則 DNS A 記錄必須解析為組織中某部 Standard Edition Server 的 IP 位址。

  - Admin 簡單 URL 僅限內部使用。如果您已部署 Director，則需要有一筆 DNS A 記錄，並讓其將 URL 解析為 Director 的 IP 位址。否則，即應解析為前端集區的負載平衡器的 IP 位址。如果您未部署集區，且使用 Standard Edition Server 部署，則 DNS A 記錄必須解析為組織中某部 Standard Edition Server 的 IP 位址。

## 簡單 URL 選項 2

在選項 2 中，Meet、Dial-in 和 Admin 簡單 URL 全都使用同一個基底 URL，例如 lync.contoso.com。因此，這些簡單 URL 只需要有一筆 DNS A 記錄，並讓其將 lync.contoso.com 解析為 Director 集區或前端集區的 IP 位址即可。如果您未部署集區，且使用 Standard Edition Server 部署，則 DNS A 記錄必須解析為組織中某部 Standard Edition Server 的 IP 位址。

請注意，如果組織中有多個 SIP 網域，您仍必須為每個 SIP 網域建立 Meet 簡單 URL，且每個 Meet 簡單 URL 各需有一筆 DNS A 記錄。在此範例中，除了有三個全都以 lync.contoso.com 為基礎的簡單 URL 外，還有一個針對 fabrikam.com 所設定，使用不同基底 URL 的 Meet 簡單 URL。在這個範例中，您必須為 https://lync.contoso.com 和 https://lync.fabrikam.com 各建立 DNS A 記錄。簡單 URL 選項 3 顯示當有多個 SIP 網域時，另一個處理命名和 DNS A 記錄的方式。

### 簡單 URL 選項 2

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>簡單 URL</strong></p></td>
<td><p><strong>範例</strong></p></td>
</tr>
<tr class="even">
<td><p>會議 (Meet)</p></td>
<td><p>https://lync.contoso.com/Meet、https://lync.fabrikam.com/Meet 等等 (組織中的每個 SIP 網域各一個)</p></td>
</tr>
<tr class="odd">
<td><p>撥入</p></td>
<td><p>https://lync.contoso.com/Dialin</p></td>
</tr>
<tr class="even">
<td><p>Admin</p></td>
<td><p>https://lync.contoso.com/Admin</p></td>
</tr>
</tbody>
</table>


## 簡單 URL 選項 3

如果您有許多 SIP 網域，且想要每個網域各有不同的簡單 URL，但想要減少這些簡單 URL 的 DNS 記錄和憑證需求，則採用選項 3 最適合。在此範例中，您僅需要有一筆 DNS A 記錄，並讓其將 lync.contoso.com 解析為 Director 集區或前端集區的 IP 位址。

### 簡單 URL 選項 3

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>簡單 URL</strong></p></td>
<td><p><strong>範例</strong></p></td>
</tr>
<tr class="even">
<td><p>會議 (Meet)</p></td>
<td><p>https://lync.contoso.com/contosoSIPdomain/Meet</p>
<p>https://lync.contoso.com/fabrikamSIPdomain/Meet</p></td>
</tr>
<tr class="odd">
<td><p>撥入</p></td>
<td><p>https://lync.contoso.com/contosoSIPdomain/Dialin</p></td>
</tr>
<tr class="even">
<td><p>Admin</p></td>
<td><p>https://lync.contoso.com/contosoSIPdomain/Admin</p></td>
</tr>
</tbody>
</table>


## 簡單 URL 的災害復原選項

如果有多個包含 前端集區的網站，且 DNS 提供者支援 GeoDNS，則可設定簡單 URL 的 DNS 記錄來支援災害復原，使得即使整個 前端集區失效，簡單 URL 功能仍可繼續。此災害復原功能支援 Meet 及 Dial-In 簡單 URL。

如要如此設定，請建立兩個 GeoDNS 位址。每個位址都包含兩個 DNS A 或 CNAME 記錄，這兩個記錄會解析為針對災害復原目的而配對的兩個集區。一個 GeoDNS 位址用於內部存取，並解析為該兩個集區的內部 Web FQDN 或負載平衡器 IP 位址。另一個 GeoDNS 位址用於外部存取，並解析為該兩個集區的外部 Web FQDN 或負載平衡器 IP 位址。下列範例針對 Meet 簡單 URL，並使用集區的 FQDN。

  ```
  Meet-int.geolb.contoso.com
       Pool1InternalWebFQDN.contoso.com
       Pool2InternalWebFQDN.contoso.com
  ```     

  ```
  Meet-ext.geolb.contoso.com
       Pool1ExternalWebFQDN.contoso.com
       Pool2ExternalWebFQDN.contoso.com
  ```     

然後建立 CNAME 記錄，其中會將 Meet 簡單 URL (例如 meet.contoso.com) 解析為兩個 GeoDNS 位址。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果網路使用 <em>「髮夾」</em> (將所有簡單 URL 流量透過外部連結路由，包括來自組織內的流量)，則可僅設定外部 GeoDNS 位址，並將 Meet 簡單 URL 僅解析為該外部位址。</td>
</tr>
</tbody>
</table>


使用此方法時，可設定每個 GeoDNS 位址使用循環配置資源方法來散發要求至兩個集區，或者主要連線至一個集區 (例如地理位置上較近的集區)，然後僅在連線失敗時才使用另一個集區。

針對 Dial-In 簡單 URL 也可以設定相同的組態。如要如此設定，請如以上範例建立其他記錄，在 DNS 記錄中用 `dialin` 替代 `meet`。針對 Admin 簡單 URL，請使用本節中先前列出的三個選項。

此組態一旦設定，就必須使用監控應用程式，設定 HTTP 監控以監看失敗。針對外部存取，請監控以確定至該兩個集區之外部 Web FQDN 或負載平衡器 IP 位址的 HTTPS GET 自動探索要求是否成功。例如，下列要求不得包含任何 **ACCEPT** 標頭且必須傳回 **200 OK**。

    HTTPS GET Pool1ExternalWebFQDN.contoso.com/autodiscover/autodiscoverservice.svc/root
    HTTPS GET Pool2ExternalWebFQDN.contoso.com/autodiscover/autodiscoverservice.svc/root

針對內部存取，則必須監控該兩個集區之內部 Web FQDN 或負載平衡器 IP 位址的連接埠 5061。如果偵測到任何連線失敗，這些集區的 VIP 必須關閉連接埠 80、443 及 444。

