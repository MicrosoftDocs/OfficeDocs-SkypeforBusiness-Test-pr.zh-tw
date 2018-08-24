---
title: Lync Server 2013：連接埠摘要 - 反向 Proxy
TOCTitle: 連接埠摘要 - 反向 Proxy
ms:assetid: 59b9ac3c-3e6f-4776-b366-174f0dd1f2eb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204932(v=OCS.15)
ms:contentKeyID: 49291011
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的連接埠摘要 - 反向 Proxy

 

_**上次修改主題的時間：** 2015-03-09_

反向 Proxy 對於防火牆和連接埠/通訊協定具有最低需求。

  - 外部防火牆需求為 HTTPS/TCP/443 和選用的 HTTP/TCP/80。HTTPS 是用於透過反向 Proxy 的 SSL 和 TLS 安全通訊。當修改憑證可能過於困難或不符成本時，若您選擇允許存取自動探索服務，則會使用 HTTP。

  - 用戶端會預期透過 HTTPS 連絡 Office Web Apps Server。 Office Web Apps Server 會預期來自內部用戶端的通訊透過 HTTPS/TCP/443。建議的設定是允許從反向 Proxy 至 Office Web Apps Server 透過 HTTPS/TCP/443。

  - 連接埠 8080 是用來將流量從反向 Proxy 內部介面路由傳送至 前端伺服器、 前端集區虛擬 IP (VIP)，或是選用的 Director 或 Director 集區 VIP。連接埠 TCP 8080 對於執行 Lync 的行動裝置而言是必要的，如此，裝置才可以在不適合修改外部 Web 服務發行規則憑證的情況下 (例如，具有大量 SIP 網域時)，用來尋找自動探索服務。如果您選擇取得含有必要 SAN 項目的新憑證，則不需要使用連接埠 TCP 8080，其為選用項目。

  - 連接埠 4443 適用於從反向 Proxy 內部介面到 前端伺服器、 前端集區虛擬 IP (VIP)，或是選用的 Director 或 Director 集區 VIP 的流量
    
    ![反向 Proxy 和外部 Web 服務](images/JJ204932.13142405-d5c9-45b7-a8b7-a8c89f09c97c(OCS.15).jpg "反向 Proxy 和外部 Web 服務")  
    
    > [!CAUTION]
    > 請勿將來自反向 Proxy 的 4443 (透過 TCP) 與來自 Standard Edition Server 或管理 中央管理存放區角色之 前端集區的連接埠 4443 (透過 TCP) 流量的內部部署混淆。


## 連接埠和通訊協定詳細資訊

### 反向 Proxy 伺服器的防火牆詳細資訊：外部介面

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
<th>附註</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HTTP/TCP/80</p></td>
<td><p>任何一個</p></td>
<td><p>反向 Proxy 接聽程式</p></td>
<td><p>(選用) 在使用者輸入 http://<em>&lt;publishedSiteFQDN&gt;</em> 時重新導向至 HTTPS。</p>
<p>在組織不希望修改外部 Web 服務發行規則憑證的情況下，如果針對會議使用 Office Web Apps 且針對執行 Lync 的行動裝置使用自動探索服務，也會需要此項目。</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP/443</p></td>
<td><p>任何一個</p></td>
<td><p>反向 Proxy 接聽程式</p></td>
<td><p>通訊錄下載、通訊錄 Web 查詢服務、自動探索、用戶端更新、會議內容、裝置更新、群組擴充、適用於會議、電話撥入式會議與會議的 Office Web Apps。</p></td>
</tr>
</tbody>
</table>


### 反向 Proxy 伺服器的防火牆詳細資訊：內部介面

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
<th>附註</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HTTP/TCP/8080</p></td>
<td><p>內部反向 Proxy 介面</p></td>
<td><p>前端伺服器、 前端集區、 Director、 Director 集區</p></td>
<td><p>在組織希望修改外部 Web 服務發行規則憑證的情況下，如果針對執行 Lync 的行動裝置使用自動探索服務，會需要此項目。</p>
<p>傳送至反向 Proxy 外部介面之連接埠 80 的流量，會從反向 Proxy 內部介面重新導向至連接埠 8080 上的集區，讓集區 Web 服務能夠將它與內部 Web 流量區分開來。</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP/4443</p></td>
<td><p>內部反向 Proxy 介面</p></td>
<td><p>前端伺服器、 前端集區、 Director、 Director 集區</p></td>
<td><p>傳送至反向 Proxy 外部介面之連接埠 443 上的流量，系統會重新導向至來自反向 Proxy 內部介面之連接埠 4443 上的集區，因此集區 Web 服務可以將它與內部 Web 流量分開來。</p></td>
</tr>
<tr class="odd">
<td><p>HTTPS/TCP/443</p></td>
<td><p>內部反向 Proxy 介面</p></td>
<td><p>適用於會議的 Office Web Apps</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

