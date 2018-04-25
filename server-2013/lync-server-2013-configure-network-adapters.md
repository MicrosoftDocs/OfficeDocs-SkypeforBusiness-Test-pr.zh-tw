---
title: Lync Server 2013：設定網路介面卡
TOCTitle: 設定網路介面卡
ms:assetid: 6519ed80-020f-47a3-851c-03dea5eac5d9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429707(v=OCS.15)
ms:contentKeyID: 49291133
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定網路介面卡

 

_**上次修改主題的時間：** 2013-11-07_

您必須指派一或多個 IP 位址給外部網路介面卡，同時至少指派一個 IP 位址給內部網路介面卡。

在下列程序中，執行 Forefront Threat Management Gateway (TMG) 2010 或 Internet Information Server Application Request Routing 的伺服器有兩張網路介面卡：

  - 公用 (外部) 網路介面卡，適用於嘗試連線至您的網站之用戶端 (亦即，通常是透過網際網路)。

  - 私人 (內部) 網路介面，適用於主控 Web 服務之執行 Lync Server 的內部伺服器。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如同 Edge Server，您僅在外部網路介面卡設定預設閘道。預設閘道會是將流量導向網際網路之路由器或對外防火牆的 IP 位址。對於從反向 Proxy 至對內網路介面卡的流量，必須將持續的靜態路由 (例如 Windows Server 中的 route 命令) 使用於包含由 Web 發行規則參照之伺服器的所有子網路。設定持續路由不會使得電腦變為路由器。如果沒有啟用 IP 轉送，電腦就只會將目的地為其他網路的特定流量導向到適當介面。實質上來說，如此會設定兩個閘道：一個做為預設閘道，指向外部網路，另一個用於目的地為內部介面的流量，位於路由器或其他網路之上。<br />
然而，如果將網路的路由器設定為摘要路由，可能不需要為所有子網路建立持續路由。建立連線至已定義路由器之網路的持續路由，然後使用該路由器為預設閘道。如果不確定網路的設定方式，而且對需要建立的持續路由需要指引，請諮詢您公司的網路工程師。<br />
反向 Proxy 必須可以解析內部 Director 或 前端伺服器 的 DNS 主機 (A) 記錄，以及用於 Web 發行規則中的下一個躍點集區 FQDN。在使用 Edge Server 時，基於安全性考量，建議您不要設定反向 Proxy 使用位於內部網路中的 DNS 伺服器。這表示在周邊中需要 DNS 伺服器，或者，需要會將每個 FQDN 解析為伺服器內部 IP 位址且位於反向 Proxy 上的 HOST 檔案項目。</td>
</tr>
</tbody>
</table>


## 設定反向 Proxy 電腦的網路介面卡

1.  在作為反向 Proxy 執行的 Windows Server 2008、 Windows Server 2008 R2、 Windows Server 2012 或 Windows Server 2012 R2 伺服器上，按一下 \[開始\] 並指向 \[控制台\] ，然後依序按一下 **\[網路和共用中心\]** 及 \[變更介面卡設定\] ，以開啟 \[變更介面卡設定\] 。

2.  以滑鼠右鍵按一下要用於外部介面的外部網路連線，然後按一下 **\[內容\]** 。

3.  在 **\[內容\]** 頁面上，按一下 **\[網路\]** 索引標籤，並按一下 **\[這個連線使用下列項目\]** 清單中的 **\[網際網路通訊協定第 4 版 (TCP/IPv4)\]** ，然後按一下 **\[內容\]** 。

4.  在 **\[網際網路通訊協定 (TCP/IP) 內容\]** 頁面上，視需要設定網路介面卡所連接網路子網路的 IP 位址。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果其他使用 HTTPS/TCP/443 的應用程式 (如用於發行 Outlook Web Access) 已使用反向 Proxy，則需要新增另一個 IP 位址以在 HTTPS/TCP/443 上發行 Lync Server 2013 Web 服務，而不干擾現有規則及 Web 接聽程式，或是需要將現有憑證取代為將新外部 FQDN 名稱新增至主體替代名稱的憑證。</td>
    </tr>
    </tbody>
    </table>


5.  按一下 **\[確定\]** ，然後再按一下 **\[確定\]** 。

6.  在 **\[網路連線\]** 中，以滑鼠右鍵按一下要用於內部介面的內部網路連線，然後按一下 **\[內容\]** 。

7.  重複步驟 3 到 5，設定內部網路連線。

