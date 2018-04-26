---
title: Lync Server 2013：連接埠摘要 - 單一合併 Edge (使用 NAT 透過私人 IP 位址)
TOCTitle: 連接埠摘要 - 單一合併 Edge (使用 NAT 透過私人 IP 位址)
ms:assetid: 3c1a389f-5f42-4719-a05b-e0b84aa3eb9e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425891(v=OCS.15)
ms:contentKeyID: 49290658
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的連接埠摘要 - 單一合併 Edge (使用 NAT 透過私人 IP 位址)

 

_**上次修改主題的時間：** 2015-03-09_

此案例架構中描述的 Lync Server 2013Edge Server 功能與 Lync Server 2010 實作的功能極為類似。最明顯的新增功能是針對 Extensible Messaging and Presence Protocol (XMPP) 的連接埠 **5269 over TCP** 項目。 Lync Server 2013 可選擇在 Edge Server 或 Edge 集區上部署 XMPP Proxy，並在 前端伺服器或 前端集區上部署 XMPP 閘道伺服器。

除了 IPv4， Edge Server 現在還可支援 IPv6。為清楚說明，案例中僅會使用 IPv4。

**具備私人 IP 定址 (使用 NAT) 之單一合併 Edge Server 的網路周邊**

![單一合併 Edge Server](images/Gg425891.f8c144c5-e5fb-498a-823e-eb39f26b6847(OCS.15).jpg "單一合併 Edge Server")

## 連接埠和通訊協定詳細資訊

建議您僅針對要提供給外部存取的功能，開啟支援所需的連接埠。

若要讓任何 Edge Service 的遠端存取能正常運作，就必須允許 SIP 流量雙向流動，如輸入/輸出 Edge 流量圖中所示。換句話說，立即訊息 (IM)、目前狀態、Web 會議、音訊/視訊 (A/V) 與同盟都牽涉到 SIP 與 Access Edge Service 的訊息往來。

### 具備私人 IP 位址 (使用 NAT) 之單一合併 Edge 的防火牆摘要：外部介面

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
<td><p>存取/HTTP/TCP/80</p></td>
<td><p>Edge Server Access Edge Service</p></td>
<td><p>任何一個</p></td>
<td><p>憑證撤銷/CRL 檢查與擷取</p></td>
</tr>
<tr class="odd">
<td><p>存取/DNS/TCP/53</p></td>
<td><p>Edge Server Access Edge Service</p></td>
<td><p>任何一個</p></td>
<td><p>透過 TCP 的 DNS 查詢</p></td>
</tr>
<tr class="even">
<td><p>存取/DNS/UDP/53</p></td>
<td><p>Edge Server Access Edge Service</p></td>
<td><p>任何一個</p></td>
<td><p>透過 UDP 的 DNS 查詢</p></td>
</tr>
<tr class="odd">
<td><p>存取/SIP(TLS)/TCP/443</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server Access Edge Service</p></td>
<td><p>適用於外部使用者存取之用戶端到伺服器的 SIP 流量</p></td>
</tr>
<tr class="even">
<td><p>存取/SIP(MTLS)/TCP/5061</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server Access Edge Service</p></td>
<td><p>適用於使用 SIP 的同盟與公用 IM 連線</p></td>
</tr>
<tr class="odd">
<td><p>存取/SIP(MTLS)/TCP/5061</p></td>
<td><p>Edge Server Access Edge Service</p></td>
<td><p>任何一個</p></td>
<td><p>適用於使用 SIP 的同盟與公用 IM 連線</p></td>
</tr>
<tr class="even">
<td><p>Web 會議/PSOM(TLS)/TCP/443</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server Web Conferencing Edge Service</p></td>
<td><p>Web 會議媒體</p></td>
</tr>
<tr class="odd">
<td><p>A/V/RTP/TCP/50,000-59,999</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>任何一個</p></td>
<td><p>與執行 Office Communications Server 2007、 Office Communications Server 2007 R2、 Lync Server 2010 及 Lync Server 2013 的協力廠商進行同盟時必須使用。</p></td>
</tr>
<tr class="even">
<td><p>A/V/RTP/UDP/50,000-59,999</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>任何一個</p></td>
<td><p>只有與執行 Office Communications Server 2007 的協力廠商進行同盟時必須使用。</p></td>
</tr>
<tr class="odd">
<td><p>A/V/RTP/TCP/50,000-59,999</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>只有與執行 Office Communications Server 2007 的協力廠商進行同盟時必須使用</p></td>
</tr>
<tr class="even">
<td><p>A/V/RTP/UDP/50,000-59,999</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>只有與執行 Office Communications Server 2007 的協力廠商進行同盟時必須使用</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN、MSTURN/UDP/3478</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>任何一個</p></td>
<td><p>3478 輸出是用於判斷與 Lync Server 正在通訊的 Edge Server 版本，也用於從 Edge Server 到 Edge Server 的媒體流量。與 Lync Server 2010、Windows Live Messenger 及 Office Communications Server 2007 R2 進行同盟時，以及在公司內部署多個 Edge 集區時，必須要使用。</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN、MSTURN/UDP/3478</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>透過 UDP/3478 進行之候選項目的 STUN/TURN 交涉</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN、MSTURN/TCP/443</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server A/V Edge 服務</p></td>
<td><p>透過 TCP/443 進行之候選項目的 STUN/TURN 交涉</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN、MSTURN/TCP/443</p></td>
<td><p>Edge Server A/V Edge Service</p></td>
<td><p>任何一個</p></td>
<td><p>透過 TCP/443 進行之候選項目的 STUN/TURN 交涉</p></td>
</tr>
</tbody>
</table>


### 具備私人 IP 位址 (使用 NAT) 之單一合併 Edge 的防火牆摘要：內部介面

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
<td><p>任何一個 (可定義為 Standard Edition 伺服器 IP、 Standard Edition 伺服器 IP 位址，或執行 XMPP 閘道服務的集區 IP 位址)</p></td>
<td><p>Edge Server 內部介面</p></td>
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
<td><p>任何一個 (可定義為 前端伺服器 IP 位址，或 前端集區中的各個 前端伺服器 IP 位址)</p>
<p></p></td>
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


## 防火牆摘要 – 公用即時訊息連線


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

