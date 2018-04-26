---
title: Lync Server 2013：外部使用者存取的憑證需求
TOCTitle: 外部使用者存取的憑證需求
ms:assetid: d45b6b10-556f-4b10-b1a7-fb0d0a64a498
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398920(v=OCS.15)
ms:contentKeyID: 49292439
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的外部使用者存取的憑證需求

 

_**上次修改主題的時間：** 2012-09-08_

Microsoft Lync Server 2013  通訊軟體支援針對 Access 和 Web Conferencing Edge 外部介面以及 A/V 驗證服務使用單一公用憑證。Edge 內部介面通常使用內部憑證授權單位 (CA) 發出的私人憑證，但是也可以使用公用憑證 (假設它來自信任的公用 CA)。您部署中的反向 Proxy 使用公共憑證，並使用 HTTP (即透過 HTTP 的傳輸層安全性)，以加密反向 Proxy 至用戶端以及反向 Proxy 至內部伺服器之間的通訊。

以下為用於 Access 和 Web Conferencing Edge 外部介面以及 A/V 驗證服務之公用憑證的需求：

  - 憑證必須由支援主體別名的認可公用 CA 發行。如需詳細資訊，請參閱 Microsoft 知識庫文件 929395＜Exchange Server 和 Communications Server 的整合通訊憑證夥伴＞，網址為 <http://go.microsoft.com/fwlink/?linkid=202834>。

  - 如果憑證將於 Edge 集區上使用，則必須建立為可匯出，並且於 Edge 集區中的每一部 Edge Server 上使用相同憑證。可匯出的私密金鑰需求是用於 A/V 驗證服務，此服務必須在集區的所有 Edge Server 中使用相同的私密金鑰。

  - 如果您想要音訊/視訊服務的上線時間達到最長，請檢閱實作低耦合 A/V Edge 服務 憑證的憑證需求 (也就是說，來自其他外部邊緣憑證用途的個別 A/V Edge 服務 憑證)。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中會影響 Edge Server 規劃的變更](lync-server-2013-changes-in-lync-server-that-affect-edge-server-planning.md), [在 Lync Server 2013 中規劃 Edge Server 憑證](lync-server-2013-plan-for-edge-server-certificates.md)＞與＜ [於 Set-CsCertificate 使用 -Roll 以預備 Lync Server 2013 中的 AV 與 OAuth 憑證](lync-server-2013-staging-av-and-oauth-certificates-using-roll-in-set-cscertificate.md)＞。

  - 憑證的主體名稱是 Access Edge Service 外部介面完整網域名稱 (FQDN) 或硬體負載平衡器 VIP (例如，access.contoso.com)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Server 2013 已不再是必要項，但是仍建議使用以提供與 Office Communications Server 的相容性。</td>
    </tr>
    </tbody>
    </table>


  - 主體別名清單包含下列各項的 FQDN：
    
      - Access Edge Service 外部介面或硬體負載平衡器 VIP (例如 sip.contoso.com)。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>即使憑證主題名稱相當於存取 Edge FQDN，主體別名仍必須包含存取 Edge FQDN，因為傳輸層安全性 (TLS) 會忽略主體名稱並且使用主體別名項目進行驗證。</td>
        </tr>
        </tbody>
        </table>
    
      - Web 會議 Edge 外部介面或硬體負載平衡器 VIP (例如，webcon.contoso.com)。
    
      - 如果您使用用戶端自動設定或同盟，則也要包含公司內使用的任何 SIP 網域 FQDN (例如 sip.contoso.com、sip.fabrikam.com)。
    
      - A/V Edge 服務不使用主體名稱或主體替代名稱項目。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>主題別名清單中 FQDN 的順序不拘。</td>
    </tr>
    </tbody>
    </table>


如果您要在網站上部署多部負載平衡 Edge Server，則每一部 Edge Server 上安裝的 A/V 驗證服務憑證都必須來自相同的 CA，而且必須使用相同的私密金鑰。請注意，無論是在一部 Edge Server 或多部 Edge Server 上使用，憑證的私密金鑰都必須可匯出。如果您從 Edge Server 以外的任何電腦要求憑證，也同樣必須是可匯出的憑證。由於 A/V 驗證服務不使用主體名稱或主體替代名稱，因此只要主體名稱和主體替代名稱需求符合 Access Edge 和 Web Conferencing Edge，且可以匯出憑證的私密金鑰，就可以重複使用 Access Edge 憑證。

Edge 內部介面所使用的私人 (或公用) 憑證之需求如下：

  - 憑證可以由內部 CA 或認可的公用憑證 CA 發行。

  - 憑證的主題名稱通常是 Edge 內部介面 FQDN 或硬體負載平衡器 VIP (例如 lsedge.contoso.com)。不過，您可以在 Edge 內部使用萬用字元憑證。

  - 不需要主體別名清單。

您部署服務中的反向 Proxy 要求：

  - 外部使用者存取會議的會議內容

  - 外部使用者存取展開並顯示通訊群組成員

  - 外部使用者存取通訊錄服務中的可下載檔案

  - 外部使用者存取 Lync Web App 用戶端

  - 外部使用者存取電話撥入式會議設定網頁

  - 外部使用者存取位置資訊服務

  - 外部裝置存取裝置更新服務並取得更新

反向 Proxy 發行內部伺服器 Web 元件 URL。Web 元件 URL 是在 Director、 前端伺服器或 前端集區上定義的，在 拓撲產生器中作為 **外部 Web 服務**。

指派給反向 Proxy 之憑證的主體替代名稱欄位支援萬用字元項目。如需如何設定反向 Proxy 之憑證要求的詳細資訊，請參閱＜ [在 Lync Server 2013 中要求及設定反向 HTTP Proxy 的憑證](lync-server-2013-request-and-configure-a-certificate-for-your-reverse-http-proxy.md)＞。

## 請參閱

#### 概念

[Lync Server 2013 中的萬用字元憑證支援](lync-server-2013-wildcard-certificate-support.md)

