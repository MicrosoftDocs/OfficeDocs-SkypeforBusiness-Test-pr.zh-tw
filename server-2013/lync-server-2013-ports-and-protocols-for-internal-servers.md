---
title: Lync Server 2013：內部伺服器的連接埠與通訊協定
TOCTitle: 內部伺服器的連接埠與通訊協定
ms:assetid: c94063f1-e802-4a61-be90-022fc185335e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398833(v=OCS.15)
ms:contentKeyID: 49292293
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 內部伺服器的連接埠與通訊協定

 

_**上次修改主題的時間：** 2015-03-09_

本節摘要說明在 Lync Server 部署中伺服器、負載平衡器和用戶端所使用的連接埠與通訊協定。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync 和 Communicator 用戶端在用於一對一通訊時，通常稱為對等通訊。技術上而言，兩個用戶端是在一對一的交談中進行通訊，以立即訊息多點控制設備 (IMMCU) 做為中介。IMMCU 是 前端伺服器 的元件。將 IMMCU 置於所需的通訊工作流程，可讓詳細通話記錄及 前端伺服器 啟用的其他功能得以使用。通訊是從用戶端上的動態來源連接埠，通向 前端伺服器 連接埠 TLS/TCP/5061 (假設使用建議的傳輸層安全性)。依照預設，對等通訊 (以及多方 IM) 只有在 Lync Server 和 IMMCU 啟用且可以使用的狀態下才能進行。</td>
</tr>
</tbody>
</table>


## 連接埠和通訊協定詳細資訊

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Windows 防火牆必須在執行中，您才能啟動伺服器上的 Lync Server 服務，因為 Lync Server 在這種情況下才能開啟防火牆的必要連接埠。</td>
</tr>
</tbody>
</table>


如需有關 Edge 元件的防火牆組態的詳細資訊，請參閱[決定 Lync Server 2013 的外部 A/V 防火牆和連接埠需求](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md)。

下表列出了在每個內部伺服器角色上需要開啟的連接埠。

### 必要的伺服器連接埠 (依伺服器角色)

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>伺服器角色</th>
<th>服務名稱</th>
<th>連接埠</th>
<th>通訊協定</th>
<th>附註</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>所有伺服器</p></td>
<td><p>SQL 瀏覽器</p></td>
<td><p>1434</p></td>
<td><p>UDP</p></td>
<td><p>複寫到本機上的中央管理存放區資料庫複本適用的 SQL 瀏覽器。</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 前端服務</p></td>
<td><p>5060</p></td>
<td><p>TCP</p></td>
<td><p>(選用) 由 Standard Edition Server 和前端伺服器用於信任服務的靜態路由，例如遠端呼叫控制伺服器。</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 前端服務</p></td>
<td><p>5061</p></td>
<td><p>TCP (TLS)</p></td>
<td><p>由 Standard Edition Server 和前端集區用於各伺服器之間 (MTLS)、伺服器與用戶端之間 (TLS) 和前端伺服器與中繼伺服器之間 (MTLS) 的所有內部 SIP 通訊。還用於與監控伺服器的通訊。</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 前端服務</p></td>
<td><p>444</p></td>
<td><p>HTTPS</p>
<p>TCP</p></td>
<td><p>用於 Focus (負責管理會議狀態的 Lync Server 元件) 與個別伺服器之間的 HTTPS 通訊。</p>
<p>此連接埠也用於 Survivable Branch Appliance 與前端伺服器之間的 TCP 通訊。</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 前端服務</p></td>
<td><p>135</p></td>
<td><p>DCOM 和遠端程序呼叫 (RPC)</p></td>
<td><p>用於以 DCOM 為基礎的作業，例如移動使用者、使用者複寫器同步和通訊錄同步。</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器</p></td>
<td><p>Lync Server IM 會議服務</p></td>
<td><p>5062</p></td>
<td><p>TCP</p></td>
<td><p>用於立即訊息 (IM) 會議的傳入 SIP 要求。</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器</p></td>
<td><p>Lync Server Web 會議服務</p></td>
<td><p>8057</p></td>
<td><p>TCP (TLS)</p></td>
<td><p>用於聆聽來自用戶端的持續性共用物件模型 (PSOM) 連線。</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器</p></td>
<td><p>Lync Server Web 會議相容性服務</p></td>
<td><p>8058</p></td>
<td><p>TCP (TLS)</p></td>
<td><p>用於聆聽來自 Live Meeting 用戶端和舊版 Lync Server 的持續性共用物件模型 (PSOM) 連線。</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 音訊/視訊會議服務</p></td>
<td><p>5063</p></td>
<td><p>TCP</p></td>
<td><p>用於音訊/視訊 (A/V) 會議的傳入 SIP 要求。</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 音訊/視訊會議服務</p></td>
<td><p>57501-65535</p></td>
<td><p>TCP/UDP</p></td>
<td><p>用於視訊會議的媒體連接埠範圍。</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器</p></td>
<td><p>Lync Server Web 相容性服務</p></td>
<td><p>80</p></td>
<td><p>HTTP</p></td>
<td><p>用於在未使用 HTTPS 時，源自前端伺服器並通往 Web 伺服陣列 FQDN (IIS Web 元件所使用的 URL) 的通訊。</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器</p></td>
<td><p>Lync Server Web 相容性服務</p></td>
<td><p>443</p></td>
<td><p>HTTPS</p></td>
<td><p>用於源自前端伺服器並通往 Web 伺服陣列 FQDN (IIS Web 元件所使用的 URL) 的通訊。</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器</p></td>
<td><p>Lync Server Web 相容性服務</p></td>
<td><p>8080</p></td>
<td><p>TCP 及 HTTP</p></td>
<td><p>供 Web 元件用於進行外部存取。</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器</p></td>
<td><p>Web 伺服器元件</p></td>
<td><p>4443</p></td>
<td><p>HTTPS</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器</p></td>
<td><p>Web 伺服器元件</p></td>
<td><p>8060</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>前端伺服器</p></td>
<td><p>Web 伺服器元件</p></td>
<td><p>8061</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器</p></td>
<td><p>Mobility Service 元件</p></td>
<td><p>5086</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p>Mobility Service 內部程序使用的 SIP 連接埠。</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器</p></td>
<td><p>Mobility Service 元件</p></td>
<td><p>5087</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p>Mobility Service 內部程序使用的 SIP 連接埠。</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器</p></td>
<td><p>Mobility Service 元件</p></td>
<td><p>443</p></td>
<td><p>HTTPS</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 會議服務員服務 (電話撥入式會議)</p></td>
<td><p>5064</p></td>
<td><p>TCP</p></td>
<td><p>用於電話撥入式會議的傳入 SIP 要求。</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 會議服務員服務 (電話撥入式會議)</p></td>
<td><p>5072</p></td>
<td><p>TCP</p></td>
<td><p>用於 Attendant 的傳入 SIP 要求 (電話撥入式會議)。</p></td>
</tr>
<tr class="even">
<td><p>還執行組合的中繼伺服器的前端伺服器</p></td>
<td><p>Lync Server 中繼服務</p></td>
<td><p>5070</p></td>
<td><p>TCP</p></td>
<td><p>由中繼伺服器用於從前端伺服器到中繼伺服器的傳入要求。</p></td>
</tr>
<tr class="odd">
<td><p>還執行組合的中繼伺服器的前端伺服器</p></td>
<td><p>Lync Server 中繼服務</p></td>
<td><p>5067</p></td>
<td><p>TCP (TLS)</p></td>
<td><p>用於從 PSTN 閘道到中繼伺服器的傳入 SIP 要求。</p></td>
</tr>
<tr class="even">
<td><p>還執行組合的中繼伺服器的前端伺服器</p></td>
<td><p>Lync Server 中繼服務</p></td>
<td><p>5068</p></td>
<td><p>TCP</p></td>
<td><p>用於從 PSTN 閘道到中繼伺服器的傳入 SIP 要求。</p></td>
</tr>
<tr class="odd">
<td><p>還執行組合的中繼伺服器的前端伺服器</p>
<p></p></td>
<td><p>Lync Server 中繼服務</p>
<p></p></td>
<td><p>5081</p></td>
<td><p>TCP</p></td>
<td><p>用於從中繼伺服器到 PSTN 閘道的傳出 SIP 要求。</p></td>
</tr>
<tr class="even">
<td><p>還執行組合的中繼伺服器的前端伺服器</p>
<p></p></td>
<td><p>Lync Server 中繼服務</p>
<p></p></td>
<td><p>5082</p></td>
<td><p>TCP (TLS)</p></td>
<td><p>用於從中繼伺服器到 PSTN 閘道的傳出 SIP 要求。</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 應用程式共用服務</p></td>
<td><p>5065</p></td>
<td><p>TCP</p></td>
<td><p>用於應用程式共用的傳入 SIP 聆聽要求。</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 應用程式共用服務</p></td>
<td><p>49152-65535</p></td>
<td><p>TCP</p></td>
<td><p>用於應用程式共用的媒體連接埠範圍。</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 會議宣告服務</p></td>
<td><p>5073</p></td>
<td><p>TCP</p></td>
<td><p>用於 Lync Server 會議宣告服務 (即電話撥入式會議) 的傳入 SIP 要求。</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 通話駐留服務</p></td>
<td><p>5075</p></td>
<td><p>TCP</p></td>
<td><p>用於通話駐留應用程式的傳入 SIP 要求。</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 音訊測試服務</p></td>
<td><p>5076</p></td>
<td><p>TCP</p></td>
<td><p>用於音訊測試服務的傳入 SIP 要求。</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器</p></td>
<td><p>不適用</p></td>
<td><p>5066</p></td>
<td><p>TCP</p></td>
<td><p>用於傳出增強型 9-1-1 (E9-1-1) 閘道。</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 回應群組服務</p></td>
<td><p>5071</p></td>
<td><p>TCP</p></td>
<td><p>用於回應群組應用程式的傳入 SIP 要求。</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 回應群組服務</p></td>
<td><p>8404</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p>用於回應群組應用程式的傳入 SIP 要求。</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 頻寬原則服務</p></td>
<td><p>5080</p></td>
<td><p>TCP</p></td>
<td><p>用於 A/V Edge TURN 流量的頻寬原則服務的通話許可控制。</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器</p></td>
<td><p>Lync Server 頻寬原則服務</p></td>
<td><p>448</p></td>
<td><p>TCP</p></td>
<td><p>用於 Lync Server 頻寬原則服務的通話許可控制。</p></td>
</tr>
<tr class="odd">
<td><p>中央管理存放區所在的前端伺服器</p></td>
<td><p>Lync Server 主要複寫器代理程式服務</p></td>
<td><p>445</p></td>
<td><p>TCP</p></td>
<td><p>用於將設定資料從中央管理存放區推送到執行 Lync Server 的伺服器。</p></td>
</tr>
<tr class="even">
<td><p>所有伺服器</p></td>
<td><p>SQL 瀏覽器</p></td>
<td><p>1434</p></td>
<td><p>UDP</p></td>
<td><p>本機 SQL Server 執行個體中中央管理存放區資料本機複寫複本的 SQL 瀏覽器。</p></td>
</tr>
<tr class="odd">
<td><p>所有內部伺服器</p></td>
<td><p>各種</p></td>
<td><p>49152-57500</p></td>
<td><p>TCP/UDP</p></td>
<td><p>用於所有內部伺服器的音訊會議的媒體連接埠範圍。由終止音訊的所有伺服器使用：前端伺服器 (用於 Lync Server 會議服務員服務、Lync Server 會議宣告服務和 Lync Server 音訊/視訊會議服務) 和中繼伺服器。</p></td>
</tr>
<tr class="even">
<td><p>Office Web Apps Server</p></td>
<td><p></p></td>
<td><p>443</p></td>
<td><p></p></td>
<td><p>由 Lync Server 2013 用來連接至 Office Web Apps Server。</p></td>
</tr>
<tr class="odd">
<td><p>Director</p></td>
<td><p>Lync Server 前端服務</p></td>
<td><p>5060</p></td>
<td><p>TCP</p></td>
<td><p>(選用) 用於信任服務的靜態路由，例如遠端呼叫控制伺服器。</p></td>
</tr>
<tr class="even">
<td><p>Director</p></td>
<td><p>Lync Server 前端服務</p></td>
<td><p>444</p></td>
<td><p>HTTPS</p>
<p>TCP</p></td>
<td><p>前端和 Director 之間的伺服器間通訊。此外，用戶端憑證發行 (至前端伺服器) 或驗證用戶端憑證是否已經發行。</p></td>
</tr>
<tr class="odd">
<td><p>Director</p></td>
<td><p>Lync Server Web 相容性服務</p></td>
<td><p>80</p></td>
<td><p>TCP</p></td>
<td><p>用於從 Director 到 Web 伺服器陣列 FQDN (IIS Web 元件所使用的 URL) 的初始通訊。在正常作業中，將切換為 HTTPS 流量，使用連接埠 443 和通訊協定類型 TCP。</p></td>
</tr>
<tr class="even">
<td><p>Director</p></td>
<td><p>Lync Server Web 相容性服務</p></td>
<td><p>443</p></td>
<td><p>HTTPS</p></td>
<td><p>用於從 Director 到 Web 伺服器陣列 FQDN (IIS Web 元件所使用的 URL) 的通訊。</p></td>
</tr>
<tr class="odd">
<td><p>Director</p></td>
<td><p>Lync Server 前端服務</p></td>
<td><p>5061</p></td>
<td><p>TCP</p></td>
<td><p>用於各伺服器間的內部通訊和用戶端連線。</p></td>
</tr>
<tr class="even">
<td><p>中繼伺服器</p></td>
<td><p>Lync Server 中繼服務</p></td>
<td><p>5070</p></td>
<td><p>TCP</p></td>
<td><p>由中繼伺服器用於來自前端伺服器的傳入要求。</p></td>
</tr>
<tr class="odd">
<td><p>中繼伺服器</p></td>
<td><p>Lync Server 中繼服務</p></td>
<td><p>5067</p></td>
<td><p>TCP (TLS)</p></td>
<td><p>用於來自 PSTN 閘道的傳入 SIP 要求。</p></td>
</tr>
<tr class="even">
<td><p>中繼伺服器</p></td>
<td><p>Lync Server 中繼服務</p></td>
<td><p>5068</p></td>
<td><p>TCP</p></td>
<td><p>用於來自 PSTN 閘道的傳入 SIP 要求。</p></td>
</tr>
<tr class="odd">
<td><p>中繼伺服器</p></td>
<td><p>Lync Server 中繼服務</p></td>
<td><p>5070</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p>用於來自前端伺服器的 SIP 要求。</p></td>
</tr>
<tr class="even">
<td><p>常設聊天室前端伺服器</p></td>
<td><p>常設聊天室 SIP</p></td>
<td><p>5041</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>常設聊天室前端伺服器</p></td>
<td><p>常設聊天室 Windows Communication Foundation (WCF)</p></td>
<td><p>881</p></td>
<td><p>TCP (TLS) 及 TCP (MTLS)</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>常設聊天室前端伺服器</p></td>
<td><p>常設聊天室檔案傳輸服務</p></td>
<td><p>443</p></td>
<td><p>TCP (TLS)</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>某些遠端通話控制案例需要前端伺服器或 Director 與 PBX 之間有 TCP 連線。儘管 Lync Server 不再使用 TCP 連接埠 5060，但在遠端通話控制部署期間您將建立受信任伺服器設定，它將 RCC 線路伺服器 FQDN 關聯至前端伺服器或 Director 用來連接到 PBX 系統的 TCP 連接埠。如需詳細資訊，請參閱 Lync Server 管理命令介面 文件中的 <strong>CsTrustedApplicationComputer</strong> Cmdlet。</td>
</tr>
</tbody>
</table>


對於只使用硬體負載平衡 (不是 DNS 負載平衡) 的集區，下表將顯示需要開啟硬體負載平衡器的連接埠。

### 硬體負載平衡器連接埠 (如果只使用硬體負載平衡)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>負載平衡器</th>
<th>連接埠</th>
<th>通訊協定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>前端伺服器負載平衡器</p></td>
<td><p>5061</p></td>
<td><p>TCP (TLS)</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器負載平衡器</p></td>
<td><p>444</p></td>
<td><p>HTTPS</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器負載平衡器</p></td>
<td><p>135</p></td>
<td><p>DCOM 和遠端程序呼叫 (RPC)</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器負載平衡器</p></td>
<td><p>80</p></td>
<td><p>HTTP</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器負載平衡器</p></td>
<td><p>8080</p></td>
<td><p>TCP - 擷取自前端伺服器根憑證的用戶端和裝置；用戶端和裝置由 NTLM 驗證</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器負載平衡器</p></td>
<td><p>443</p></td>
<td><p>HTTPS</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器負載平衡器</p></td>
<td><p>4443</p></td>
<td><p>HTTPS (反向 Proxy)</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器負載平衡器</p></td>
<td><p>5072</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器負載平衡器</p>
<p></p></td>
<td><p>5073</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器負載平衡器</p>
<p></p></td>
<td><p>5075</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器負載平衡器</p>
<p></p></td>
<td><p>5076</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器負載平衡器</p>
<p></p></td>
<td><p>5071</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器負載平衡器</p>
<p></p></td>
<td><p>5080</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器負載平衡器</p>
<p></p></td>
<td><p>448</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="odd">
<td><p>中繼伺服器負載平衡器</p>
<p></p></td>
<td><p>5070</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器負載平衡器 (如果集區還執行中繼伺服器)</p>
<p></p></td>
<td><p>5070</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="odd">
<td><p>Director 負載平衡器</p></td>
<td><p>443</p></td>
<td><p>HTTPS</p></td>
</tr>
<tr class="even">
<td><p>Director 負載平衡器</p></td>
<td><p>444</p></td>
<td><p>HTTPS</p></td>
</tr>
<tr class="odd">
<td><p>Director 負載平衡器</p>
<p></p></td>
<td><p>5061</p></td>
<td><p>TCP</p></td>
</tr>
<tr class="even">
<td><p>Director 負載平衡器</p></td>
<td><p>4443</p></td>
<td><p>HTTPS (反向 Proxy)</p></td>
</tr>
</tbody>
</table>


使用 DNS 負載平衡的前端集區和 Director 集區還必須部署硬體負載平衡器。下表顯示了在這些硬體負載平衡器上需要開啟的連接埠。

### 硬體負載平衡器連接埠 (如果使用 DNS 負載平衡)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>負載平衡器</th>
<th>連接埠</th>
<th>通訊協定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>前端伺服器負載平衡器</p></td>
<td><p>80</p></td>
<td><p>HTTP</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器負載平衡器</p></td>
<td><p>443</p></td>
<td><p>HTTPS</p></td>
</tr>
<tr class="odd">
<td><p>前端伺服器負載平衡器</p></td>
<td><p>8080</p></td>
<td><p>TCP - 擷取自前端伺服器根憑證的用戶端和裝置；用戶端和裝置由 NTLM 驗證</p></td>
</tr>
<tr class="even">
<td><p>前端伺服器負載平衡器</p></td>
<td><p>4443</p></td>
<td><p>HTTPS (反向 Proxy)</p></td>
</tr>
<tr class="odd">
<td><p>Director 負載平衡器</p></td>
<td><p>443</p></td>
<td><p>HTTPS</p></td>
</tr>
<tr class="even">
<td> </td>
<td> </td>
<td> </td>
</tr>
<tr class="odd">
<td><p>Director 負載平衡器</p></td>
<td><p>4443</p></td>
<td><p>HTTPS (反向 Proxy)</p></td>
</tr>
</tbody>
</table>


### 必要的用戶端連接埠

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>元件</th>
<th>連接埠</th>
<th>通訊協定</th>
<th>附註</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>用戶端</p></td>
<td><p>67/68</p></td>
<td><p>DHCP</p></td>
<td><p>由 Lync Server 用於尋找登錄器 FQDN (即如果 DNS SRV 失敗且未設定手動設定)。</p></td>
</tr>
<tr class="even">
<td><p>用戶端</p>
<p></p></td>
<td><p>443</p></td>
<td><p>TCP (TLS)</p></td>
<td><p>用於外部使用者存取的用戶端到伺服器 SIP 流量。</p></td>
</tr>
<tr class="odd">
<td><p>用戶端</p></td>
<td><p>443</p></td>
<td><p>TCP (PSOM/TLS)</p></td>
<td><p>用於外部使用者存取 Web 會議工作階段。</p></td>
</tr>
<tr class="even">
<td><p>用戶端</p></td>
<td><p>443</p></td>
<td><p>TCP (STUN/MSTURN)</p></td>
<td><p>用於外部使用者存取 A/V 工作階段與媒體 (TCP)。</p></td>
</tr>
<tr class="odd">
<td><p>用戶端</p></td>
<td><p>3478</p></td>
<td><p>UDP (STUN/MSTURN)</p></td>
<td><p>用於外部使用者存取 A/V 工作階段與媒體 (UDP)。</p></td>
</tr>
<tr class="even">
<td><p>用戶端</p></td>
<td><p>5061</p></td>
<td><p>TCP (MTLS)</p></td>
<td><p>用於外部使用者存取的用戶端到伺服器 SIP 流量。</p></td>
</tr>
<tr class="odd">
<td><p>用戶端</p></td>
<td><p>6891-6901</p></td>
<td><p>TCP</p></td>
<td><p>用於 Lync 用戶端與舊版用戶端 (Microsoft Office Communications Server 2007 R2、Microsoft Office Communications Server 2007 和 Live Communications Server 2005 的用戶端) 之間的檔案傳輸。</p></td>
</tr>
<tr class="even">
<td><p>用戶端</p></td>
<td><p>1024-65535 *</p></td>
<td><p>TCP/UDP</p></td>
<td><p>音訊連接埠範圍 (最少需要 20 個連接埠)。</p></td>
</tr>
<tr class="odd">
<td><p>用戶端</p></td>
<td><p>1024-65535 *</p></td>
<td><p>TCP/UDP</p>
<p></p></td>
<td><p>視訊連接埠範圍 (最少需要 20 個連接埠)。</p></td>
</tr>
<tr class="even">
<td><p>用戶端</p></td>
<td><p>1024-65535 *</p></td>
<td><p>TCP</p></td>
<td><p>對等檔案傳輸 (對於會議檔案傳輸，用戶端使用 PSOM)。</p></td>
</tr>
<tr class="odd">
<td><p>用戶端</p></td>
<td><p>1024-65535 *</p></td>
<td><p>TCP</p></td>
<td><p>應用程式共用。</p></td>
</tr>
<tr class="even">
<td><p>Aastra 6721ip 公共區域電話</p>
<p>Aastra 6725ip 電話機</p>
<p>HP 4110 IP Phone (公共區域電話)</p>
<p>HP 4120 IP Phone (電話機)</p>
<p>Polycom CX500 IP 公共區域電話</p>
<p>Polycom CX600 IP 電話機</p>
<p>Polycom CX700 IP 電話機</p>
<p>Polycom CX3000 IP 會議電話</p></td>
<td><p>67/68</p></td>
<td><p>DHCP</p></td>
<td><p>由列出的裝置用於尋找 Lync Server 憑證、佈建 FQDN 和登錄器 FQDN。</p></td>
</tr>
</tbody>
</table>


**\*** 若要為這些媒體類型設定特定連接埠，請使用 CsConferencingConfiguration Cmdlet (ClientMediaPortRangeEnabled、ClientMediaPort 以及 ClientMediaPortRange 參數)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync 用戶端的設定程式將自動在用戶端電腦上建立所需的作業系統防火牆例外狀況。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在用戶端必須周遊組織的防火牆 (例如，由其他組織主持的外部通訊或會議) 的情況下，需要有外部使用者存取要使用的連接埠。</td>
</tr>
</tbody>
</table>

