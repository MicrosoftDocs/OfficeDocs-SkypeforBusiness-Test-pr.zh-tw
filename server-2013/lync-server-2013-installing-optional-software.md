---
title: Lync Server 2013：安裝選用軟體
TOCTitle: 安裝選用軟體
ms:assetid: b95b3301-fa1e-4b96-9af4-05b43d39db8d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615032(v=OCS.15)
ms:contentKeyID: 52056188
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中安裝選用軟體

 

_**上次修改主題的時間：** 2013-02-21_

Microsoft Lync Server 2013 規劃工具設計為匯出至 Microsoft Excel 和 Microsoft Visio。雖然這些應用程式不是 規劃工具的作業所必要，但確實為您設計的部署和文件帶來相當程度的價值。

## 選用軟體

## Microsoft Excel

將您的設計匯出至 Microsoft Excel 會建立一份報表，其試算表中會顯示七個索引標籤：

  - 摘要 – 顯示有關網站組態的資訊，包括使用者計數、容量設定和伺服器設定檔資訊。

  - 硬體設定檔 – 顯示有關拓撲中所指定伺服器之建議硬體組態的報表，包括 CPU、記憶體、磁碟和網路介面。伺服器元件的數量和建議的規格亦包括在內。此外，每一部伺服器都會依網站定義，以便依網站完整表示伺服器需求。

  - 連接埠需求 – 顯示所有已啟用連接埠的報表，以及與網域名稱系統負載平衡 (DNS LB) 和硬體負載平衡器 (HLB) 的關聯。此報表應用於規劃您的防火牆和 DNS LB 與 HLB 組態。

  - 摘要報告 – 顯示需要設定 Edge Server 網路的一般設定摘要。

  - 憑證報告 – 顯示必須執行 Edge Server 之憑證所需的主體名稱和主體別名。

  - 防火牆報告 – 顯示外部和內部介面的來源、目的地及 IP 位址。

  - DNS 報告 – 為您所建立的每個 DNS 項目顯示所需的完整網域名稱 (FQDN) 和 IP/VIP 位址。

## Microsoft Visio

將您的設計匯出至 Microsoft Visio 會建立一個圖表，可用於您所設定拓撲和基礎結構的文件。匯入的圖表可以依照您的文件需要加以編輯和重新排列。一般 Visio 圖表包括：

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您的設計規模夠大，需要超過三部前端伺服器，則會針對 前端集區、 前端伺服器以及執行 SQL Server、IP 位址和 FQDN 的電腦另外建立一個頁面。</td>
</tr>
</tbody>
</table>


  - 通用拓撲 – 已設定 Lync Server 2013 網站的圖表。

  - 網站名稱索引標籤 – 顯示網站組態拓撲，其中包括 Edge Server、防火牆、公用交換電話網路 (PSTN) 與閘道，以及內部伺服器部署。內部部署由設定的伺服器和集區所組成，包括前端集區、SQL Server 架構伺服器、Active Directory 網域服務、Director、Exchange Unified Messaging (UM) 伺服器、Exchange 信箱伺服器、Office Web Apps Server、中繼伺服器及常設聊天室伺服器。

  - 邊緣網路圖 – 顯示詳細 Edge Server 組態與相關 IP 位址及 FQDN 的圖表。DNS 負載平衡和硬體負載平衡器亦包含在內。此外，也會顯示 Director 與前端伺服器或前端集區，以及相關聯的 DNS LB 或 HLB 和指派的 IP 位址 (規劃工具 可同時支援 IPv4 和 IPv6 位址) 及 FQDN。

## 請參閱

#### 工作

[在 Lync Server 2013 中安裝規劃工具](lync-server-2013-installing-the-planning-tool.md)

