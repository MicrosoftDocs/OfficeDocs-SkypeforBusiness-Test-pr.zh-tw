---
title: Lync Server 2013：反向 Proxy 案例
TOCTitle: 反向 Proxy 案例
ms:assetid: 13108f59-a660-4ff1-8404-079d1cb646f2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204691(v=OCS.15)
ms:contentKeyID: 49290159
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的反向 Proxy 案例

 

_**上次修改主題的時間：** 2013-01-21_

Lync Server 2013 中需要反向 Proxy 才可供存取服務及資源，例如會議和撥入簡單 URL、通訊錄、會議內容、通訊群組清單延伸、行動服務等等。 Lync Server 2013 中典型的反向 Proxy 案例是允許外部用戶端 (例如，桌面用戶端或 Lync Web App 用戶端) 存取 Director 或 前端伺服器外部 Web 服務。

**反向 Proxy 和外部 Web 服務**

![反向 Proxy 和外部 Web 服務](images/JJ204932.13142405-d5c9-45b7-a8b7-a8c89f09c97c(OCS.15).jpg "反向 Proxy 和外部 Web 服務")

您會在規劃階段期間定義 Lync Server 2013 部署中反向 Proxy 的需求。反向 Proxy 可讓下列外部用戶端存取功能︰

  - Microsoft Lync 2013 桌面用戶端

  - Microsoft Lync Web App

  - Microsoft Lync Mobile

  - Lync Windows 市集應用程式

您在規劃 Lync Server 2013 部署時，會將 Lync Server 2013 的實際需求對應到反向 Proxy 功能。

1.  外部用戶端會從連接埠 TCP 443 連線到反向 Proxy，並使用安全通訊端層 (SSL) 或傳輸層安全性 (TLS)。 Microsoft Lync Mobile 用戶端可以從連接埠 TCP 80 連線，但只有在執行初始連線至 Lync 探索服務，且系統管理員已設定適當的網域名稱系統 (DNS) CNAME (或別名) 記錄，並接受該通訊不會進行加密的情況下。

2.  Lync Server 2013 外部 Web 服務 (部署於 前端伺服器及/或 Director) 會預期反向 Proxy 連線至連接埠 TCP 4443，並且預期連線為 SSL/TLS。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>建議用於外部 Web 服務的預設聆聽連接埠為 TCP 8080 用於 HTTP 流量，TCP 4443 用於 HTTPS 流量。 拓撲產生器可用於覆寫預設值並自行定義外部 Web 服務的聆聽連接埠。需要注意的是，反向 Proxy 是與外部 Web 服務通訊，而外部用戶端是與反向 Proxy 通訊。外部用戶端會從連接埠 TCP 443 與反向 Proxy 通訊，但您可重新定義反向 Proxy 與外部 Web 服務通訊的連接埠。 拓撲產生器中覆寫 Web 服務預設聆聽連接埠的選項，可讓您解決基礎結構中可能發生的聆聽連接埠衝突。</td>
    </tr>
    </tbody>
    </table>


3.  Lync Server 2013 外部 Web 服務會預期來自用戶端之未修改過的主機標頭，以識別用戶端想要使用的服務和 Web 伺服器目錄。要求應會顯示為如同來自反向 Proxy。

4.  外部 Web 服務會使用已定義的 Web 伺服器虛擬目錄 (vDir) 來提供服務給用戶端。特定外部可識別的 Web 服務為︰
    
      - 用於網路會議的 "Meet" vDir
    
      - 用於電話存取和電話會議的 "Dialin" vDir
    
      - 用於 Lync Windows 市集應用程式、 Lync Mobile 及桌面用戶端 Lync 2013 的 "Autodiscover" vDir。 Lync Server 2013 中自動探索是以 DNS 名稱 "lyncdiscover" 為名。
    
      - 外部用戶端若要存取未定義的服務，則會直接呼叫外部 Web 服務。例如，通訊群組延伸 (DLX) 和通訊錄服務 (ABS) 是透過直接呼叫外部 Web 服務及關聯的 vDir 進行存取的。用戶端知道通往 vDir 的實際路徑，會根據該資訊建構統一記錄定位器 (URL)。用戶端會使用類似 `https://externalweb.contoso.com/abs/handler` 的 URL 來存取通訊錄服務
    
      - Office Web Apps Server，當會議定義並設定為 Lync Server 拓撲的一部分時
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Office Web Apps Server 是個別的角色伺服器，並且未設為外部 Web 服務的一部分。此伺服器是個別發行供用戶端存取。</td>
        </tr>
        </tbody>
        </table>


5.  定義各服務的 SSL 橋接。外部連接埠 TCP 443 會對應至外部 Web 服務連接埠 TCP 4443。對於未加密的 HTTP，連接埠 TCP 80 會對應至外部 Web 服務連接埠 TCP 8080

6.  規劃反向 Proxy 接聽程式以發行 Web 伺服器資源

7.  根據所要提供的服務，要求並設定反向 Proxy 的憑證。若設定正確的主體替代名稱，則反向 Proxy 伺服器上所有設定的接聽程式皆可共用此憑證

可用來規劃反向 Proxy 部署的資源：

  - [Lync Server 2013 中的資料收集](lync-server-2013-data-collection.md)

  - [Lync Server 2013 中的憑證摘要 - 反向 Proxy](lync-server-2013-certificate-summary-reverse-proxy.md)

  - [Lync Server 2013 中的連接埠摘要 - 反向 Proxy](lync-server-2013-port-summary-reverse-proxy.md)

  - [Lync Server 2013 中的 DNS 摘要 - 反向 Proxy](lync-server-2013-dns-summary-reverse-proxy.md)

