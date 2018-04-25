---
title: Lync Server 2013：主控 Exchange UM 整合架構
TOCTitle: 主控 Exchange UM 整合架構
ms:assetid: 0094d5dc-1836-441c-b6e2-f88e35203a8d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398067(v=OCS.15)
ms:contentKeyID: 49289891
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的主控 Exchange UM 整合架構

 

_**上次修改主題的時間：** 2012-09-25_

Lync Server 2013 ExUM Routing 應用程式支援與下列項目的整合：內部部署 Exchange 整合通訊 (UM)、服務提供者提供的託管式 Exchange UM，或這兩者的綜合。下圖顯示所有這三種可能性。

**與內部部署 Exchange UM 和兩個託管式 Exchange 提供者整合**

![內部部署 Lync Server Exchange UM 部署](images/Gg398821.d6498eb9-87ee-40f3-8ecd-852f91546590(OCS.15).jpg "內部部署 Lync Server Exchange UM 部署")

支援下列模式：

  - **內部部署 ：** Lync Server 2013 和 Exchange UM 都部署於您企業內的本機伺服器上。

  - **交叉部署 ：** Lync Server 2013 部署於您企業內的本機伺服器上，而 Exchange UM 裝載於線上服務提供者的設備中 (如 Microsoft Exchange 線上資料中心)。

  - **混合部署 ：** Lync Server 2013 部署中有一些使用者信箱位於您企業內的本機 Exchange 伺服器上，有一些信箱位於託管式 Exchange 服務資料中心。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>混合部署可以作為過渡解決方案 (例如進行評估以及將使用者分階段移轉至託管式 Exchange UM 的期間) 或永久解決方案 (如果您在進行部分移轉後，決定將其餘使用者的 Exchange UM 服務繼續留在內部部署)。</td>
    </tr>
    </tbody>
    </table>


## 共用 SIP 位址空間

若要整合 Lync Server 2013 與內部部署 Exchange UM，您必須授與 Lync Server 2013 權限以讀取 Exchange UM Active Directory 網域服務物件。但是，此方法不適用於與託管式 Exchange UM 的整合，因為 Lync Server 2013 和 Exchange UM 是分別安裝於兩個沒有互信的樹系中。

若要整合 Lync Server 2013 與託管式 Exchange UM，您必須設定「共用 SIP 位址空間」 。在此組態中，同一個 SIP 網域位址空間可同時供 Lync Server 2013 和託管式 Exchange UM 服務提供者使用。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>共用 SIP 位址空間的使用方法，類似於交叉部署 Lync Server 2013 環境，即一些使用者位於內部部署，一些使用者位於託管式部署 (如 Lync Online)。SIP 網域被這兩者分割。當您整合 Lync Server 2013 與託管式 Exchange UM 時，請務必將 Exchange UM 服務提供者包含在共用 SIP 位址空間中。</td>
</tr>
</tbody>
</table>


若要設定共用 SIP 位址空間以便與 Exchange UM 服務提供者整合，您必須如下設定 Edge Server：

1.  設定 Edge Server 進行同盟，作法為執行 **Set-CsAccessEdgeConfiguration** Cmdlet 以設定下列參數：
    
      - **UseDnsSrvRouting** 指定 Edge Server 傳送和接收同盟要求時將依賴 DNS SRV 記錄。
    
      - **AllowFederatedUsers** 指定是否允許內部使用者與同盟網域的使用者進行通訊。此屬性也會判斷內部使用者是否可與分割網域案例中的使用者進行通訊。
    
      - **EnablePartnerDiscovery** 指定 Lync Server 2013 是否使用 DNS 記錄來嘗試探索未列在 Active Directory 允許網域清單中的協力廠商網域。如果是 False， Lync Server 2013 只會與已列在允許網域清單上的網域進行同盟。如果使用 DNS 服務路由，則需要此參數。在大多數部署中，此值設定為 False，以免對所有合作夥伴開放同盟。

2.  將 中央管理存放區複寫至 Edge Server 並確認複寫成功。如需詳細資訊，請參閱部署文件中的＜ [匯出 Lync Server 2013 拓撲並將拓撲複製到 Edge 安裝的外部媒體](lync-server-2013-export-your-topology-and-copy-it-to-external-media-for-edge-installation.md)＞。

3.  在 Edge Server 上設定 *「裝載提供者」* ，作法是執行 **New-CsHostingProvider** Cmdlet 以設定下列參數：
    
      - **Identity** 為所建立的裝載提供者指定唯一的字串值識別碼，例如 **Hosted Exchange UM** 。
    
      - **Enabled** 指出網域與裝載提供者之間的網路連線是否已啟用。必須設定為 **True** 。
    
      - **EnabledSharedAddressSpace** 指出是否將以共用 SIP 位址空間案例使用裝載提供者。必須設定為 **True** 。
    
      - **HostsOCSUsers** 指出裝載提供者是否用於裝載 Lync Server 2013 帳戶。必須設定為 **False** 。
    
      - **ProxyFQDN** 指定裝載提供者所使用之 Proxy 伺服器的完整網域名稱 (FQDN)，例如 **proxyserver.fabrikam.com** 。如需此資訊，請與您的裝載提供者連絡。您無法修改此值。如果裝載提供者變更其 Proxy 伺服器，您必須刪除再重新建立該提供者的項目。
    
      - **IsLocal** 指出裝載提供者使用的 Proxy 伺服器是否包含在您的 Lync Server 2013 拓撲內。必須設定為 **False**。

