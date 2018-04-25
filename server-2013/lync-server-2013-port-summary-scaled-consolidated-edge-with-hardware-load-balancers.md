---
title: Lync Server 2013：連接埠摘要 - 調整式合併 Edge (利用硬體負載平衡器)
TOCTitle: 連接埠摘要 - 調整式合併 Edge (利用硬體負載平衡器)
ms:assetid: 91213b1e-f875-464b-83e8-fe3a351595a4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398739(v=OCS.15)
ms:contentKeyID: 49291668
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的連接埠摘要 - 調整式合併 Edge (利用硬體負載平衡器)

 

_**上次修改主題的時間：** 2015-04-27_

Lync Server 2013 (此案例架構中所述的 Edge Server 功能) 非常類似 Lync Server 2010 中實作的 Edge Server 功能。最值得注意的新增功能是適用於可延伸傳訊和顯示狀態通訊協定 (XMPP) 的連接埠 **5269 over TCP** 項目。 Lync Server 2013 可以選擇性地在 Edge Server 或 Edge 集區上部署 XMPP Proxy，以及在 前端伺服器或 前端集區上部署 XMPP 閘道伺服器。

除了 IPv4， Edge Server 現在還可支援 IPv6。為清楚說明，案例中僅會使用 IPv4。

**使用硬體負載平衡調整合併 Edge**

![Edge Server 周邊網路連接埠與通訊協定](images/Gg398739.063f7dd1-16db-4cc7-8708-bca9bc41184d(OCS.15).jpg "Edge Server 周邊網路連接埠與通訊協定")

## 連接埠和通訊協定詳細資訊

建議您僅針對要提供給外部存取的功能開放支援所需的連接埠。

若要讓遠端存取可在任何 Edge Service 上運作，SIP 流量必須能夠雙向流動，如輸入/輸出 Edge 流量圖所示。換句話說，往返於 Access Edge Service 的 SIP 訊息會涉及立即訊息 (IM)、顯示狀態、Web 會議、音訊/視訊 (A/V) 及同盟等功能。

### 調整式合併 Edge (硬體負載平衡) 的防火牆摘要：外部介面 - 節點 1 與節點 2 (範例)

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
<td><p>存取/HTTP/TCP/80</p></td>
<td><p>Adresse IP publique du Access Edge Service du Edge Server</p></td>
<td><p>任何一個</p></td>
<td><p>憑證撤銷/CRL 檢查與擷取</p></td>
</tr>
<tr class="even">
<td><p>存取/DNS/TCP/53</p></td>
<td><p>Adresse IP publique du Access Edge Service du Edge Server</p></td>
<td><p>任何一個</p></td>
<td><p>透過 TCP 的 DNS 查詢</p></td>
</tr>
<tr class="odd">
<td><p>存取/DNS/UDP/53</p></td>
<td><p>Adresse IP publique du Access Edge Service du Edge Server</p></td>
<td><p>任何一個</p></td>
<td><p>透過 UDP 的 DNS 查詢</p></td>
</tr>
<tr class="even">
<td><p>A/V/RTP/TCP/50,000-59,999</p></td>
<td><p>Edge Server  A/V Edge 服務 IP 位址</p></td>
<td><p>任何一個</p></td>
<td><p>與執行 Office Communications Server 2007、 Office Communications Server 2007 R2、 Lync Server 2010 及 Lync Server 2013 的協力廠商進行同盟時必須使用。</p></td>
</tr>
<tr class="odd">
<td><p>A/V/RTP/UDP/50,000-59,999</p></td>
<td><p>Edge Server A/V Edge 服務 公用 IP 位址</p></td>
<td><p>任何一個</p></td>
<td><p>只有與執行 Office Communications Server 2007 的協力廠商進行同盟時必須使用。</p></td>
</tr>
<tr class="even">
<td><p>A/V/RTP/TCP/50,000-59,999</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server A/V Edge 服務 公用 IP 位址</p></td>
<td><p>只有與執行 Office Communications Server 2007 的協力廠商進行同盟時必須使用</p></td>
</tr>
<tr class="odd">
<td><p>A/V/RTP/UDP/50,000-59,999</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server A/V Edge 服務 公用 IP 位址</p></td>
<td><p>只有與執行 Office Communications Server 2007 的協力廠商進行同盟時必須使用</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN、MSTURN/UDP/3478</p></td>
<td><p>Edge Server A/V Edge 服務 公用 IP 位址</p></td>
<td><p>任何一個</p></td>
<td><p>3478 輸出用於決定與 Lync Server 通訊的 Edge Server 版本，同時也用於從 Edge Server 至 Edge Server 的媒體流量。 與 Lync Server 2010、Windows Live Messenger 及 Office Communications Server 2007 R2 進行同盟時，以及在公司內部署多個 Edge 集區時，必須要使用。</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN、MSTURN/UDP/3478</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server A/V Edge 服務 公用 IP 位址</p></td>
<td><p>透過 UDP/3478 進行之候選項目的 STUN/TURN 交涉</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN、MSTURN/TCP/443</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server A/V Edge 服務 公用 IP 位址</p></td>
<td><p>透過 TCP/443 進行之候選項目的 STUN/TURN 交涉</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN、MSTURN/TCP/443</p></td>
<td><p>Edge Server A/V Edge 服務 公用 IP 位址</p></td>
<td><p>任何一個</p></td>
<td><p>透過 TCP/443 進行之候選項目的 STUN/TURN 交涉</p></td>
</tr>
</tbody>
</table>


### 調整式合併 Edge (硬體負載平衡) 的防火牆摘要：內部介面節點 1 與節點 2

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
<td><p>XMPP/MTLS/TCP/23456</p></td>
<td><p>任何一個 (可定義為 前端伺服器位址，或執行 XMPP 閘道服務的 前端集區虛擬 IP 位址)</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>在 前端伺服器或 前端集區上執行之 XMPP 閘道服務的輸出 XMPP 流量</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP/4443</p></td>
<td><p>任何 (可以定義為保有 中央管理存放區之 前端伺服器的伺服器 IP 或集區)</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>將變更從 中央管理存放區複寫到 Edge Server</p></td>
</tr>
<tr class="odd">
<td><p>PSOM/MTLS/TCP/8057</p></td>
<td><p>任何 (可以定義為 Director IP、 前端伺服器 IP 或集區虛擬 IP)</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>從內部部署到內部 Edge Server 介面的 Web 會議流量</p></td>
</tr>
<tr class="even">
<td><p>STUN/MSTURN/UDP/3478</p></td>
<td><p>任何 (可以定義為 Director IP、 前端伺服器 IP 或集區虛擬 IP)</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>內部與外部使用者之間 A/V 媒體傳輸的慣用路徑， Survivable Branch Appliance 或 Survivable Branch 伺服器</p></td>
</tr>
<tr class="odd">
<td><p>STUN/MSTURN/TCP/443</p></td>
<td><p>任何 (可以定義為 Director IP、 前端伺服器 IP 或集區虛擬 IP)</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>如果無法建立 UDP 通訊，TCP 用於檔案傳輸和桌面共用時，內部與外部使用者之間 A/V 媒體傳輸的後援路徑， Survivable Branch Appliance 或 Survivable Branch 伺服器</p></td>
</tr>
<tr class="even">
<td><p>MTLS/TCP/50001</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>使用 Lync Server 管理命令介面和 集中記錄服務 Cmdlet、ClsController 命令列 (ClsController.exe) 或代理程式 (ClsAgent.exe) 命令與記錄集合的 集中記錄服務控制器</p></td>
</tr>
<tr class="odd">
<td><p>MTLS/TCP/50002</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>使用 Lync Server 管理命令介面和 集中記錄服務 Cmdlet、ClsController 命令列 (ClsController.exe) 或代理程式 (ClsAgent.exe) 命令與記錄集合的 集中記錄服務控制器</p></td>
</tr>
<tr class="even">
<td><p>MTLS/TCP/50003</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server 內部介面</p></td>
<td><p>使用 Lync Server 管理命令介面和 集中記錄服務 Cmdlet、ClsController 命令列 (ClsController.exe) 或代理程式 (ClsAgent.exe) 命令與記錄集合的 集中記錄服務控制器</p></td>
</tr>
</tbody>
</table>


在部署以針對 Lync Server 提供可用性與負載平衡時，硬體負載平衡器會有特殊需求。這些需求定義於下圖和下列表格中。協力廠商可能會針對此處所定義的需求使用不同的術語。您需要將 Lync Server 的需求對應至您硬體負載平衡器廠商所提供的功能與設定選項。

設定硬體負載平衡器時，請考量下列需求：

  - 可在適用於 Access Edge Service 和 Web Conferencing Edge Service 的硬體負載平衡器 (HLB) 上設定來源網路位址轉譯 (SNAT)

  - SNAT 無法設定於 A/V Edge 服務 上 - A/V Edge 服務 必須使用真正的伺服器位址來回應，而不是 HLB 虛擬 IP (VIP)，才能讓僅透過 NAT 周遊的 UDP (STUN)/使用延遲 NAT 周遊 (TURN)/同盟 TURN (FTURN) 正確運作

  - 公用 IP 位址可用於每個伺服器介面上和 HLB 的 VIP 上，而您的公用 IP 位址需求是 N+1，其中每個真正伺服器介面都有一個公用 IP 位址，以及一個適用於每個 HLB VIP 的公用 IP 位址。若集區上有 2 部 Edge Server，就會產生 9 個公用 IP 位址，其中有 3 個是用於 HLB VIP，且每個 Edge Server 介面都會有一個公用 IP 位址 (這些伺服器總共會有 6 個位址)

  - 針對 Access Edge Service 和 Web Conferencing Edge Service (以及在 HLB 上使用 NAT)，用戶端會連絡 VIP，VIP 會將來源 IP 位址從用戶端變更為它自己的 IP 位址。伺服器介面會將傳回的位址提供給 VIP，VIP 會變更來自伺服器介面 IP 位址的來源位址，並將封包傳送給用戶端

  - 針對 A/V Edge 服務，VIP 無法變更來源 IP 位址，並會將真正的伺服器位址直接傳回給用戶端 - 您無法在 HLB 上設定適用於 AV 流量的 NAT

  - 針對 AV，外部防火牆將保留適用於所有封包的真正伺服器公用 IP 位址

  - 一旦建立之後，與 A/V Edge 服務 通訊的用戶端會是與真正伺服器進行通訊，而不是 HLB

  - 必須路由傳送對內部伺服器和用戶端的內部邊緣，並針對所有裝載伺服器或用戶端的內部網路設定持續路由

  - HLB Access Edge Service VIP 將做為每個 Edge Server 介面的預設閘道

![Edge Server 連接埠與通訊協定詳細資訊](images/Gg398739.1c193b80-98ab-4d59-a854-dbfdb5e209e2(OCS.15).jpg "Edge Server 連接埠與通訊協定詳細資訊")

### 調整式合併 Edge (硬體負載平衡) 的必要外部連接埠設定：外部介面虛擬 IP

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
<td><p>存取/SIP(TLS)/TCP/443</p></td>
<td><p>任何一個</p></td>
<td><p>Access Edge Service 公用 VIP 位址</p></td>
<td><p>適用於外部使用者存取之用戶端到伺服器的 SIP 流量</p></td>
</tr>
<tr class="even">
<td><p>存取/SIP(MTLS)/TCP/5061</p></td>
<td><p>任何一個</p></td>
<td><p>Access Edge Service 公用 VIP 位址</p></td>
<td><p>使用 SIP 的 SIP 訊號、同盟及公用 IM 連線</p></td>
</tr>
<tr class="odd">
<td><p>存取/SIP(MTLS)/TCP/5061</p></td>
<td><p>Access Edge Service 公用 VIP 位址</p></td>
<td><p>同盟協力廠商</p></td>
<td><p>使用 SIP 的 SIP 訊號、同盟及公用 IM 連線</p></td>
</tr>
<tr class="even">
<td><p>Web 會議/PSOM(TLS)/TCP/443</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server  Web Conferencing Edge Service 公用 VIP 位址</p></td>
<td><p>Web 會議媒體</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN、MSTURN/UDP/3478</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server A/V Edge 服務 公用 VIP 位址</p></td>
<td><p>透過 UDP/3478 進行之候選項目的 STUN/TURN 交涉</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN、MSTURN/TCP/443</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server A/V Edge 服務 公用 VIP 位址</p></td>
<td><p>透過 TCP/443 進行之候選項目的 STUN/TURN 交涉</p></td>
</tr>
</tbody>
</table>


### 調整式合併 Edge (硬體負載平衡) 的防火牆摘要：內部介面虛擬 IP

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
<td><p>任何一個 (可定義為 Director、 Director 集區虛擬 IP 位址、 前端伺服器或 前端集區虛擬 IP 位址)</p></td>
<td><p>Edge Server 內部 VIP 介面</p></td>
<td><p>至內部 Edge VIP 的輸出 SIP 流量 (來自 Director、 Director 集區虛擬 IP 位址、 前端伺服器或 前端集區虛擬 IP 位址)</p></td>
</tr>
<tr class="even">
<td><p>存取/SIP(MTLS)/TCP/5061</p></td>
<td><p>Edge Server 內部 VIP 介面</p></td>
<td><p>任何一個 (可定義為 Director、 Director 集區虛擬 IP 位址、 前端伺服器或 前端集區虛擬 IP 位址)</p></td>
<td><p>來自 Edge Server 內部介面的輸入 SIP 流量 (送至 Director、 Director 集區虛擬 IP 位址、 前端伺服器或 前端集區虛擬 IP 位址)</p></td>
</tr>
<tr class="odd">
<td><p>SIP/MTLS/TCP/5062</p></td>
<td><p>任何一個 (可定義為 前端伺服器 IP 位址，或 前端集區 IP 位址，或使用此 Edge Server 的任何 Survivable Branch Appliance 或 Survivable Branch 伺服器)</p></td>
<td><p>Edge Server 內部 VIP 介面</p></td>
<td><p>來自 前端伺服器或 前端集區 IP 位址，或使用此 Edge Server 之任何 Survivable Branch Appliance 或 Survivable Branch 伺服器的 A/V 使用者驗證 (A/V 驗證服務)</p></td>
</tr>
<tr class="even">
<td><p>STUN/MSTURN/UDP/3478</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server 內部 VIP 介面</p></td>
<td><p>內部與外部使用者之間 A/V 媒體傳輸的慣用路徑</p></td>
</tr>
<tr class="odd">
<td><p>STUN/MSTURN/TCP/443</p></td>
<td><p>任何一個</p></td>
<td><p>Edge Server 內部 VIP 介面</p></td>
<td><p>如果無法建立 UDP 通訊，TCP 用於檔案傳輸和桌面共用時，內部與外部使用者之間 A/V 媒體傳輸的後援路徑</p></td>
</tr>
<tr class="even">
<td><p>STUN/MSTURN/TCP/443</p></td>
<td><p>Edge Server 內部 VIP 介面</p></td>
<td><p>任何一個</p></td>
<td><p>如果無法建立 UDP 通訊，TCP 用於檔案傳輸和桌面共用時，內部與外部使用者之間 A/V 媒體傳輸的後援路徑</p></td>
</tr>
</tbody>
</table>

