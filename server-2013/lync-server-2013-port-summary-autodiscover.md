---
title: Lync Server 2013 中的連接埠摘要 - 自動探索
TOCTitle: Lync Server 2013 中的連接埠摘要 - 自動探索
ms:assetid: 8bd16363-5e18-4e4b-be99-b3e6457b4c99
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945642(v=OCS.15)
ms:contentKeyID: 52056168
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的連接埠摘要 - 自動探索

 

_**上次修改主題的時間：** 2015-03-09_

Lync Server 2013 自動探索服務會在 Director 集區和前端集區伺服器上執行，使用 `lyncdiscover.<domain>` 和 `lyncdiscoverinternal.<domain>` 主機記錄在 DNS 中發行時，可透過用戶端使用以找出 Lync Server 功能。為了讓執行 Lync Mobile 的行動裝置可使用自動探索，您需要先在任何執行自動探索服務的 Director 和前端伺服器上修改憑證主體替代名稱清單。此外，外部 Web 服務用於發行反向 Proxy 規則所使用的憑證主體替代名稱清單也可能需要修改。

是否在反向 Proxy 上使用主體替代名稱清單，取決於是在連接埠 80 還是連接埠 443 上發行自動探索服務：

  - **發行在連接埠 80 上**   對於行動裝置而言，如果對自動探索服務的初始查詢是透過連接埠 80 來進行，則不需要任何憑證變更。這是因為執行 Lync 的行動裝置會從連接埠 80 外部存取反向 Proxy，然後在連接埠 8080 內部重新導向至 Director 或前端伺服器。

  - **發行在連接埠 443 上**   外部 Web 服務發行規則所使用之憑證上的主體替代名稱清單，必須針對組織內的每個 SIP 網域，各包含一個 `lyncdiscover.<sipdomain>` 項目。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如需從您部署 Mobility 的 Lync Server 2010 上進行全新安裝或升級，可針對 Mobility 服務的自動探索使用連接埠 80，或利用適當的主體名稱及主體替代名稱重新發行憑證。請檢閱 Director 和前端伺服器上的憑證，以確認您所選擇的路徑。</td>
    </tr>
    </tbody>
    </table>


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
<td><p>(選用) 在使用者輸入 http://<em>&lt;發行網站 FQDN&gt;</em> 時重新導向至 HTTPS。在組織不希望修改外部 Web 服務發行規則憑證的情況下，如果針對會議使用 Office Web Apps 且針對執行 Lync 的行動裝置使用自動探索服務，也會需要此項目。</p></td>
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
<td><p>適用於會議的 前端伺服器、前端集區、Director、Director 集區、Office Web Apps</p></td>
<td><p>在組織不希望修改外部 Web 服務發行規則憑證的情況下，如果針對執行 Lync 的行動裝置使用自動探索服務，會需要此項目。傳送至反向 Proxy 外部介面之連接埠 80 的流量，會從反向 Proxy 內部介面重新導向至連接埠 8080 上的集區，讓集區 Web 服務能夠將它與內部 Web 流量分開來。</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP/4443</p></td>
<td><p>內部反向 Proxy 介面</p></td>
<td><p>適用於會議的 前端伺服器、前端集區、Director、Director 集區、Office Web Apps</p></td>
<td><p>傳送至反向 Proxy 外部介面之連接埠 443 上的流量，系統會重新導向至來自反向 Proxy 內部介面之連接埠 4443 上的集區，因此集區 Web 服務可以將它與內部 Web 流量分開來。</p></td>
</tr>
</tbody>
</table>

