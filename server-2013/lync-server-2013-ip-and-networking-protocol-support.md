---
title: Lync Server 2013：IP 和網路通訊協定支援
TOCTitle: IP 和網路通訊協定支援
ms:assetid: b0cffb10-3478-445c-89c7-8cb8b5027424
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412848(v=OCS.15)
ms:contentKeyID: 49292021
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 IP 和網路通訊協定支援

 

_**上次修改主題的時間：** 2012-09-21_

Lync Server 2013 支援下列 IP 和網路通訊協定：

  - **IP 通訊協定。**Lync Server 2013 支援 IP 版本 4 (IPv4) 或 IP 版本 6 (IPv6) 的伺服器網路。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Server 2013 可以在啟用雙重 IP 堆疊的網路中運作。</td>
    </tr>
    </tbody>
    </table>


  - **SIP 傳輸通訊協定。**一般而言，SIP 至少可以使用三個傳輸類型：使用者資料包通訊協定 (UDP)、傳輸控制通訊協定 (TCP)，以及傳輸層安全性 (TLS)。在預設 SIP 傳輸設定中，TLS 會透過 TCP 執行。TLS 是在 Lync Server 2013 網路內部使用。在網路邊緣， Lync Server 2013 可透過 TCP 交互操作。 Lync Server 2013 不支援將 UDP 用於 SIP 傳輸，因為它不符合企業通訊安全性、可靠性和延展性的最低標準。如需詳細資訊，請參閱 NextHop 部落格文章＜是否使用 UDP 是問題所在＞，網址為 [http://go.microsoft.com/fwlink/?linkid=185369\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=185369%26clcid=0x404)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>每個部落格的內容及其 URL 如有任何變更，恕不另行通知。</td>
    </tr>
    </tbody>
    </table>

