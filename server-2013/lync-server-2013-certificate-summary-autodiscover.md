---
title: 憑證摘要 - 自動探索
TOCTitle: 憑證摘要 - 自動探索
ms:assetid: 16ac96bb-882a-4141-b75c-9530637548d9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945616(v=OCS.15)
ms:contentKeyID: 52056058
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 憑證摘要 - 自動探索

 

_**上次修改主題的時間：** 2015-03-09_

Lync Server 2013 自動探索服務會在 Director 和前端集區伺服器上執行，而且在 DNS 中發行時，可供 Lync 用戶端用來尋找伺服器和使用者服務。若您從 Lync Server 2010 升級且未部署 Mobility Services，則在用戶端可使用自動探索之前，您必須先在任何執行自動探索服務的 Director 和前端伺服器上修改憑證主體替代名稱清單。此外，外部 Web 服務用於發行反向 Proxy 規則所使用的憑證主體替代名稱清單也可能需要修改。

是否在反向 Proxy 上使用主體替代名稱清單，取決於是在連接埠 80 還是連接埠 443 上發行自動探索服務：

  - **在連接埠 80 上發行**   如果對自動探索服務的初始查詢是透過連接埠 80 進行，則不需要任何憑證變更。這是因為執行 Lync 的行動裝置會從連接埠 80 外部存取反向 Proxy，然後從連接埠 8080 內部橋接至 Director 或前端伺服器。如需詳細資訊，請參閱＜[Lync Server 2013 行動技術需求](lync-server-2013-technical-requirements-for-mobility.md)＞的＜初始自動探索程序使用連接埠 80＞一節。

  - **在連接埠 443 上發行**   外部 Web 服務發行規則所使用的憑證主體替代名稱清單，必須針對組織內的每個 SIP 網域，各包含一個「lyncdiscover.\<SIP 網域\>」 項目。
    
    > [!IMPORTANT]  
    > 強烈建議您使用 HTTPS，而不使用 HTTP。HTTPS 會使用憑證來加密流量。HTTP 不提供加密，且任何資料都是以純文字的方式傳送。
    


使用內部憑證授權單位來重新發出憑證通常是個簡單的程序。但是對於 Web 服務用來發行規則的公用憑證而言，新增多個主體替代名稱項目可能會變得很昂貴。為了避免這個問題，我們支援透過連接埠 80 進行初始的自動探索連線，這會重新導向至 Director 或前端伺服器上的連接埠 8080。

> [!NOTE]  
> 如果 Lync Server 2013 基礎結構使用內部憑證授權單位 (CA) 發出的內部憑證，而且您計劃要支援行動裝置以無線方式連線，則內部 CA 的根憑證鏈結必須安裝在行動裝置上，否則您就必須變更 Lync Server 2013 基礎結構使用公用憑證。



本主題說明 Director、前端伺服器及反向 Proxy 所需新增的主題替代名稱。在此僅提及新增的主體替代名稱 (SAN)。對於憑證上其他項目的指示，請參閱規劃章節。如需詳細資訊，請參閱＜[Lync Server 2013 中的 Director 案例](lync-server-2013-scenarios-for-the-director.md)、[Lync Server 2013 中的外部使用者存取案例](lync-server-2013-scenarios-for-external-user-access.md)＞，以及＜[Lync Server 2013 中的反向 Proxy 案例](lync-server-2013-scenarios-for-reverse-proxy.md)＞。

下列表格定義 Director 集區、前端集區及反向 Proxy 適用的自動探索 SAN 項目︰

### Director 集區憑證需求

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>說明</th>
<th>主體替代名稱項目</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>內部自動探索服務 URL</p></td>
<td><p>SAN=lyncdiscoverinternal.<em>&lt;內部網域名稱&gt;</em></p></td>
</tr>
<tr class="even">
<td><p>外部自動探索服務 URL</p></td>
<td><p>SAN=lyncdiscover.<em>&lt;SIP 網域&gt;</em></p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> 您可以將含有新 SAN 項目的新更新憑證指派給預設憑證。或者，您可以使用 SAN=*.<em>&lt;SIP 網域&gt;</em>。



### 前端集區憑證需求

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>說明</th>
<th>主體替代名稱項目</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>內部自動探索服務 URL</p></td>
<td><p>SAN=lyncdiscoverinternal.<em>&lt;內部網域名稱&gt;</em></p></td>
</tr>
<tr class="even">
<td><p>外部自動探索服務 URL</p></td>
<td><p>SAN=lyncdiscover.<em>&lt;SIP 網域&gt;</em></p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> 您可以將含有新 SAN 項目的新更新憑證指派給預設憑證。或者，您可以使用 SAN=*.<em>&lt;SIP 網域&gt;</em>



### 反向 Proxy (公用 CA) 憑證需求

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>說明</th>
<th>主體替代名稱項目</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>外部自動探索服務 URL</p></td>
<td><p>SAN=lyncdiscover.<em>&lt;SIP 網域&gt;</em></p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> 您可以將含有新 SAN 項目的新更新憑證指派給反向 Proxy 上的 SSL 接聽程式。


