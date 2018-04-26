---
title: Lync Server 2013：連接埠摘要 - 調整式合併 Edge (使用 NAT 透過私人 IP 位址進行 DNS 負載平衡)
TOCTitle: 連接埠摘要 - 調整式合併 Edge (使用 NAT 透過私人 IP 位址進行 DNS 負載平衡)
ms:assetid: a296c2af-54d4-4b4f-9795-9191baf688cb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412756(v=OCS.15)
ms:contentKeyID: 49291878
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的連接埠摘要 - 調整式合併 Edge (使用 NAT 透過私人 IP 位址進行 DNS 負載平衡)

 

_**上次修改主題的時間：** 2015-03-09_

Lync Server 2013 (此案例架構中所述的 Edge Server 功能) 非常類似 Lync Server 2010 中實作的 Edge Server 功能。最值得注意的新增功能是適用於可延伸傳訊和顯示狀態通訊協定 (XMPP) 的連接埠 **5269 over TCP** 項目。 Lync Server 2013 可以選擇性地在 Edge Server 或 Edge 集區上部署 XMPP Proxy，以及在 前端伺服器或 前端集區上部署 XMPP 閘道伺服器。

除了 IPv4， Edge Server 現在還可支援 IPv6。為清楚說明，案例中僅會使用 IPv4。

**具有使用 NAT 的私人 IP 位址之調整式合併 Edge 的企業周邊網路**

![調整式合併邊緣](images/JJ205394.96f5a8f5-16d2-464d-b86e-7c7ecfc89ead(OCS.15).jpg "調整式合併邊緣")

## 連接埠和通訊協定詳細資訊

建議您僅針對要提供給外部存取的功能開放支援所需的連接埠。

若要遠端存取以處理任何 Edge 服務，則必須允許雙向的 SIP 流量，如「輸出/輸入」Edge 流量圖所示。換言之，即時訊息 (IM)、目前狀態、Web 會議、音訊/視訊 (A/V) 及同盟均與來回傳輸 Access Edge 服務的 SIP 訊息有關。

### 調整式合併 Edge 的防火牆摘要，透過使用 NAT 的私人 IP 位址達到 DNS 負載平衡：外部介面 – 節點 1 和節點 2 (範例)

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>角色/通訊協定/TCP 或 UDP/連接埠</th>
<th>來源 IP 位址</th>
<th>目的地 IP 位址</th>
<th>附註</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>XMPP/TCP/5269</p></td>
<td><p>任何一個</p></td>
<td><p>XMPP Proxy 服務 (與 Access Edge Service 共用 IP 位址)</p></td>
<td><p>XMPP Proxy 服務會接收來自已定義之 XMPP 同盟中 XMPP 連絡人的流量</p></td>
</tr>
<tr class="even">
<td><p>XMPP/TCP/5269</p></td>
<td><p>XMPP Proxy 服務 (與 Access Edge Service 共用 IP 位址)</p></td>
<td><p>任何一個</p></td>
<td><p>XMPP Proxy 服務會將流量傳送至已定義 XMPP 同盟的 XMPP 連絡人</p></td>
</tr>
<tr class="odd">
<td><p>存取/HTTP/TCP/80</p></td>
<td><p>Edge Server Access Edge Service</p></td>
<td><p>任何一個</p></td>
<td><p>憑證撤銷/CRL 檢查與擷取</p></td>
</tr>
<tr class="even">
<td><p>存取/DNS/TCP/53</p></td>
<td><p>Edge Server Access Edge Service</p></td>
<td><p>任何一個</p></td>
<td><p>透過 TCP 的 DNS 查詢</p></td>
</tr>
<tr class="odd">
<td><p>存取/DNS/UDP/53</p></td>
<td><p>Edge Server Access Edge Service</p></td>
<td><p>任何一個</p></td>
<td><p>透過 UDP 的 DNS 查詢</p></td>
</tr>
<tr class="even">
<td><p>存取/SIP(TLS)/TCP/443</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server Access Edge Service</p></td>
<td><p>適用於外部使用者存取之用戶端到伺服器的 SIP 流量</p></td>
</tr>
<tr class="odd">
<td><p>存取/SIP(MTLS)/TCP/5061</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server Access Edge 服務</p></td>
<td><p>適用於使用 SIP 的同盟與公用 IM 連線</p></td>
</tr>
<tr class="even">
<td><p>存取/SIP(MTLS)/TCP/5061</p></td>
<td><p>Edge Server Access Edge Service</p></td>
<td><p>任何一個</p></td>
<td><p>適用於使用 SIP 的同盟與公用 IM 連線</p></td>
</tr>
<tr class="odd">
<td><p>Web 會議/PSOM(TLS)/TCP/443</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server Web Conferencing Edge Service</p></td>
<td><p>Web 會議媒體</p></td>
</tr>
<tr class="even">
<td><p>A/V/RTP/TCP/50,000-59,999</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>任何一個</p></td>
<td><p>與執行 Office Communications Server 2007、 Office Communications Server 2007 R2、 Lync Server 2010 及 Lync Server 2013 的協力廠商進行同盟時必須使用。</p></td>
</tr>
<tr class="odd">
<td><p>A/V/RTP/UDP/50,000-59,999</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>任何一個</p></td>
<td><p>只有與執行 Office Communications Server 2007 的協力廠商進行同盟時必須使用。</p></td>
</tr>
<tr class="even">
<td><p>A/V/RTP/TCP/50,000-59,999</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>只有與執行 Office Communications Server 2007 的協力廠商進行同盟時必須使用</p></td>
</tr>
<tr class="odd">
<td><p>A/V/RTP/UDP/50,000-59,999</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>只有與執行 Office Communications Server 2007 的協力廠商進行同盟時必須使用</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN、MSTURN/UDP/3478</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>任何一個</p></td>
<td><p>3478 輸出用於決定與 Lync Server 通訊的 Edge Server 版本，同時也用於從 Edge Server 至 Edge Server 的媒體流量。 與 Lync Server 2010、Windows Live Messenger 及 Office Communications Server 2007 R2 進行同盟時，以及在公司內部署多個 Edge 集區時，必須要使用。</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN、MSTURN/UDP/3478</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>透過 UDP/3478 進行之候選項目的 STUN/TURN 交涉</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN、MSTURN/TCP/443</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>透過 TCP/443 進行之候選項目的 STUN/TURN 交涉</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN、MSTURN/TCP/443</p></td>
<td><p>Edge Server A/V Edge Service</p></td>
<td><p>任何一個</p></td>
<td><p>透過 TCP/443 進行之候選項目的 STUN/TURN 交涉</p></td>
</tr>
</tbody>
</table>


### 調整式合併 Edge 的防火牆摘要，透過使用 NAT 的私人 IP 位址達到 DNS 負載平衡：內部介面 – 節點 1 和節點 2 (範例)

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>通訊協定/TCP 或 UDP/連接埠</th>
<th>來源 IP 位址</th>
<th>目的地 IP 位址</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>XMPP/MTLS/TCP/23456</p></td>
<td><p>任何一個 (可定義為 前端伺服器位址，或執行「XMPP 閘道」服務的 前端集區 IP 位址)</p></td>
<td><p>Edge Server 內部介面 IP 位址</p></td>
<td><p>在 前端伺服器或 前端集區上執行之 XMPP 閘道服務的輸出 XMPP 流量</p></td>
</tr>
<tr class="even">
<td><p>SIP/MTLS/TCP/5061</p></td>
<td><p>任何一個 (可定義為 Director、 Director 集區 IP 位址、 前端伺服器或 前端集區 IP 位址)</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>送至 Edge Server 內部介面的輸出 SIP 流量 (來自 Director、 Director 集區 IP 位址、 前端伺服器或 前端集區 IP 位址)</p></td>
</tr>
<tr class="odd">
<td><p>SIP/MTLS/TCP/5061</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>任何一個 (可定義為 Director、 Director 集區 IP 位址、 前端伺服器或 前端集區 IP 位址)</p></td>
<td><p>來自 Edge Server 內部介面的輸入 SIP 流量 (送至 Director、 Director 集區 IP 位址、 前端伺服器或 前端集區 IP 位址)</p></td>
</tr>
<tr class="even">
<td><p>PSOM/MTLS/TCP/8057</p></td>
<td><p>任何一個 (可定義為 前端伺服器 IP 位址，或 前端集區中的各個 前端伺服器 IP 位址)</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>從 前端伺服器或每部 前端伺服器 (若在集區內) 至 Edge Server 內部介面的 Web 會議流量</p></td>
</tr>
<tr class="odd">
<td><p>SIP/MTLS/TCP/5062</p></td>
<td><p>任何一個 (可定義為 前端伺服器 IP 位址，或 前端集區 IP 位址，或使用此 Edge Server 的任何 Survivable Branch Appliance 或 Survivable Branch 伺服器)</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>來自 前端伺服器或 前端集區 IP 位址，或使用此 Edge Server 之任何 Survivable Branch Appliance 或 Survivable Branch 伺服器的 A/V 使用者驗證 (A/V 驗證服務)</p></td>
</tr>
<tr class="even">
<td><p>STUN/MSTURN/UDP/3478</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>內部與外部使用者之間 A/V 媒體傳輸的慣用路徑， Survivable Branch Appliance 或 Survivable Branch 伺服器</p></td>
</tr>
<tr class="odd">
<td><p>STUN/MSTURN/TCP/443</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>如果無法建立 UDP 通訊，TCP 用於檔案傳輸和桌面共用時，內部與外部使用者之間 A/V 媒體傳輸的後援路徑， Survivable Branch Appliance 或 Survivable Branch 伺服器</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP/4443</p></td>
<td><p>任何一個 (可定義為 前端伺服器 IP 位址，或具備 中央管理存放區的集區)</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>將變更從 中央管理存放區複寫到 Edge Server</p></td>
</tr>
<tr class="odd">
<td><p>MTLS/TCP/50001</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>使用 Lync Server 管理命令介面和 集中記錄服務 Cmdlet、ClsController 命令列 (ClsController.exe) 或代理程式 (ClsAgent.exe) 命令與記錄集合的 集中記錄服務控制器</p></td>
</tr>
<tr class="even">
<td><p>MTLS/TCP/50002</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>使用 Lync Server 管理命令介面和 集中記錄服務 Cmdlet、ClsController 命令列 (ClsController.exe) 或代理程式 (ClsAgent.exe) 命令與記錄集合的 集中記錄服務控制器</p></td>
</tr>
<tr class="odd">
<td><p>MTLS/TCP/50003</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>使用 Lync Server 管理命令介面和 集中記錄服務 Cmdlet、ClsController 命令列 (ClsController.exe) 或代理程式 (ClsAgent.exe) 命令與記錄集合的 集中記錄服務控制器</p></td>
</tr>
</tbody>
</table>


## 同盟的防火牆摘要


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>角色/通訊協定/TCP 或 UDP/連接埠</th>
<th>來源 IP 位址</th>
<th>目的地 IP 位址</th>
<th>附註</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>存取/SIP(MTLS)/TCP/5061</p></td>
<td><p>Access Edge Service 公用 IP 位址</p></td>
<td><p>任何一個</p></td>
<td><p>適用於使用 SIP 的同盟與公用 IM 連線</p></td>
</tr>
</tbody>
</table>


## 防火牆摘要 – 公用立即訊息連線


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>角色/通訊協定/TCP 或 UDP/連接埠</th>
<th>來源 IP 位址</th>
<th>目的地 IP 位址</th>
<th>附註</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>存取/SIP(MTLS)/TCP/5061</p></td>
<td><p>公用 IM 夥伴</p></td>
<td><p>Edge Server Access Edge Service</p></td>
<td><p>適用於使用 SIP 的同盟與公用 IM 連線</p></td>
</tr>
<tr class="even">
<td><p>存取/SIP(MTLS)/TCP/5061</p></td>
<td><p>Edge Server Access Edge Service</p></td>
<td><p>公用 IM 夥伴</p></td>
<td><p>適用於使用 SIP 的同盟與公用 IM 連線</p></td>
</tr>
<tr class="odd">
<td><p>存取/SIP(TLS)/TCP/443</p></td>
<td><p>用戶端</p></td>
<td><p>Edge Server Access Edge Service</p></td>
<td><p>適用於外部使用者存取之用戶端到伺服器的 SIP 流量</p></td>
</tr>
<tr class="even">
<td><p>A/V/RTP/TCP/50,000-59,999</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>Live Messenger 用戶端</p></td>
<td><p>如果設定的是公共 IM 連線，則用於 Windows Live Messenger 的 A/V 工作階段。</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN、MSTURN/UDP/3478</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>Live Messenger 用戶端</p></td>
<td><p>公用 IM 連線的 Windows Live Messenger 必須使用</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN、MSTURN/UDP/3478</p></td>
<td><p>Live Messenger 用戶端</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>公用 IM 連線的 Windows Live Messenger 必須使用</p></td>
</tr>
</tbody>
</table>


## 可延伸訊息與目前狀態通訊協定的防火牆摘要


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>通訊協定/TCP 或 UDP/連接埠</th>
<th>來源 (IP 位址)</th>
<th>目的地 (IP 位址)</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>XMPP/TCP/5269</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server  Access Edge Service 介面 IP 位址</p></td>
<td><p>XMPP 的標準伺服器對伺服器通訊連接埠。允許從同盟 XMPP 夥伴到 Edge Server XMPP Proxy 的通訊</p></td>
</tr>
<tr class="even">
<td><p>XMPP/TCP/5269</p></td>
<td><p>Edge Server  Access Edge Service 介面 IP 位址</p></td>
<td><p>任何一個</p></td>
<td><p>XMPP 的標準伺服器對伺服器通訊連接埠。允許從 Edge Server Proxy 到同盟 XMPP 夥伴的通訊。 partners</p></td>
</tr>
<tr class="odd">
<td><p>XMPP/MTLS/TCP/23456</p></td>
<td><p>任何一個</p></td>
<td><p>每個內部 Edge Server 介面 IP</p></td>
<td><p>從 前端伺服器或 前端集區上的 XMPP 閘道，到 Edge Server 內部 IP 位址或每個 Edge 集區成員之內部 IP 位址的內部 XMPP 流量</p></td>
</tr>
</tbody>
</table>

