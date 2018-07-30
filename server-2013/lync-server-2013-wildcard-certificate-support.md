---
title: Lync Server 2013 萬用字元憑證支援
TOCTitle: 萬用字元憑證支援
ms:assetid: 0bae2aa8-b6dc-46f5-a3be-3fe7581809d4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202161(v=OCS.15)
ms:contentKeyID: 49290063
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的萬用字元憑證支援

 

_**上次修改主題的時間：** 2013-03-21_

Lync Server 2013 使用憑證來提供通訊加密以及伺服器身分識別驗證。某些情況下，例如透過反向 Proxy 的 Web 發佈，不需要與代表服務之伺服器完整網域名稱 (FQDN) 相符的強式主體替代名稱 (SAN) 項目。在這些情況下，您可以使用含萬用字元 SAN 項目的憑證 (一般稱為「萬用字元憑證」) 來降低從公用憑證授權單位要求憑證的成本，並能降低憑證的規劃程序複雜度。

<table>
<thead>
<tr class="header">
<th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要保留整合通訊 (UC) 裝置 (例如，電話機) 的功能，您應該仔細測試部署的憑證，確定實作萬用字元憑證之後，裝置的功能正常運作。</td>
</tr>
</tbody>
</table>


不支援將萬用字元項目做為任何角色的主體名稱 (又稱為一般名稱或 CN)。在 SAN 中使用萬用字元項目時，支援下列伺服器角色：

   **反向 Proxy。**   簡單 URL (Meet 和 Dial-in) 發行憑證支援萬用字元 SAN 項目。

   **反向 Proxy。**   發行憑證上的 LyncDiscover SAN 項目支援萬用字元 SAN 項目。 .

   **Director。**   簡單 URL (Meet 和 Dial-in) 和 Director Web 元件的 LyncDiscover 與 LyncDiscoverInternal SAN 項目支援萬用字元 SAN 項目。

   **前端伺服器 ( Standard Edition) 及 前端集區 ( Enterprise Edition)。**簡單 URL (Meet 和 Dial-in) 和前端 Web 元件的 LyncDiscover 與 LyncDiscoverInternal SAN 項目支援萬用字元 SAN 項目。

   **Exchange 整合通訊 (UM)。**   伺服器部署為獨立伺服器時，不使用 SAN 項目。

   **Microsoft Exchange Server Client Access Server。**   內部和外部用戶端支援 SAN 中的萬用字元項目。

   **相同伺服器上的 Exchange 整合通訊 (UM) 和 Microsoft Exchange Server Client Access Server。**   支援萬用字元 SAN 項目。

本主題中未介紹的伺服器角色：

  - 內部伺服器角色 (包括，但不限於 中繼伺服器、 封存與監控伺服器、 Survivable Branch Appliance 或 Survivable Branch 伺服器)

  - 外部 Edge Server 介面

  - 內部 Edge Server
    
    > [!NOTE]  
    > 至於內部 Edge Server 介面，可以將萬用字元項目指派給 SAN，而且可受支援。不會查詢內部 Edge Server 上的 SAN，而且萬用字元 SAN 項目的值會受到限制。
    


如需憑證設定的詳細資訊，包括在憑證中使用萬用字元，請參閱下列主題：

  - [Lync Server 2013 中內部伺服器的憑證需求](lync-server-2013-certificate-requirements-for-internal-servers.md)

  - [Lync Server 2013 中的外部使用者存取的憑證需求](lync-server-2013-certificate-requirements-for-external-user-access.md)

  - [Lync Server 2013 中的憑證摘要 - DNS 與 HLB 負載平衡](lync-server-2013-certificate-summary-dns-and-hlb-load-balanced.md)

  - [Lync Server 2013 中的憑證摘要 - 單一 Director](lync-server-2013-certificate-summary-single-director.md)

  - [Lync Server 2013 中的憑證摘要 - 調整式 Director 集區 (硬體負載平衡器)](lync-server-2013-certificate-summary-scaled-director-pool-hardware-load-balancer.md)

  - [Lync Server 2013 中的憑證摘要 - 反向 Proxy](lync-server-2013-certificate-summary-reverse-proxy.md)

  - [整合內部部署 Unified Messaging 和 Lync Server 2013 的指導方針](lync-server-2013-guidelines-for-integrating-on-premises-unified-messaging.md)

如需為 Exchange 設定憑證的詳細資訊，包括使用萬用字元，請參閱 Exchange 2013 產品文件。

