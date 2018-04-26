---
title: Lync Server 2013：如何實作 SIP 主幹？
TOCTitle: 如何實作 SIP 主幹？
ms:assetid: 273a22b1-8a4c-4187-acf8-c57d5c6598ce
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425743(v=OCS.15)
ms:contentKeyID: 49290409
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 如何在 Lync Server 2013 中實作 SIP 主幹？

 

_**上次修改主題的時間：** 2013-03-18_

若要實作 SIP 主幹，您必須透過 中繼伺服器來路由連線，以在必要時作為 Proxy 代為處理 Lync Server 2013 用戶端與服務提供者之間的通訊工作階段，以及進行媒體轉碼。

每個 中繼伺服器都有內部網路介面與外部網路介面。內部介面會連線至 前端伺服器。外部介面常被稱為閘道介面，因為過去人們都用其來將 中繼伺服器連線至公用交換電話網路 (PSTN) 閘道或 IP-PBX。若要實作 SIP 主幹，您必須將 中繼伺服器的外部介面連線至 ITSP 的外部 Edge 元件。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ITSP 的外部 Edge 元件可以是工作階段界限控制器 (SBC)、路由器或閘道。</td>
</tr>
</tbody>
</table>


如需 中繼伺服器的詳細資訊，請參閱＜ [Lync Server 2013 中的中繼伺服器元件](lync-server-2013-mediation-server-component.md)＞。

## 集中式與分散式 SIP 主幹的比較

「集中式」 SIP 主幹會透過 中央網站路由所有的 VoIP 流量，包括 分支網站流量在內。集中式部署模型既簡單又符合成本效益，是實作 SIP 主幹與 Lync Server 2013 時廣受推薦的方法。

*分散式* SIP 主幹是會在一或多個分支網站上實作本機 SIP 主幹的部署模型。接著，VoIP 流量會從 分支網站直接路由給服務提供者，而不會經由 中央網站。

只有下列情況才必須使用分散式 SIP 主幹：

  - 分支網站需要可存活的電話連線 (例如 WAN 失效時)。每個 分支網站均應就此需求進行分析：您的分支網站有些可能有備援與容錯移轉的需求，有些則否。

  - 兩個 中央網站之間必須要有恢復能力。您必須確定 SIP 主幹在每個 中央網站上均已終止。例如，如果您有 Dublin 與 Tukwila 兩個 中央網站，且兩者共用一個網站的 SIP 主幹，則在該主幹失效時，另一個網站的使用者即無法撥打 PSTN 電話。

  - 分支網站與 中央網站位於不同的國家/地區。基於相容性與法規考量，每個國家/地區至少要有一個 SIP 主幹。以歐盟地區為例，若未在中心點上進行本機終止，通訊就只能侷限在國家/地區的範圍。

根據網站所處的地理位置以及您預期企業內會有的流量，您可能不想透過中央 SIP 主幹路由所有使用者，或是會選擇透過部分使用者 分支網站上的 SIP 主幹來路由這些使用者。若要分析自身需求，請回答下列問題：

  - 每個網站的規模為何 (也就是有多少使用者能夠使用 企業語音)？

  - 各網站上的哪些直接向內撥號 (DID) 號碼來電數最多？

在考量應部署集中式或分散式 SIP 主幹時，必須進行成本效益分析。在某些情況下，即便並非必要，選擇分散式部署模型可能較有利。在完全集中式部署中，所有 分支網站流量都會透過 WAN 連結進行路由。與其為 WAN 連結所需的頻寬支付高額費用，您可能寧可使用分散式 SIP 主幹。例如，您可能會將 Standard Edition 伺服器部署在與 中央網站同盟的 分支網站上，或是使用小型閘道部署 Survivable Branch Appliance 或 Survivable Branch 伺服器。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需分散式 SIP 主幹的詳細資訊，請參閱＜ <a href="lync-server-2013-branch-site-sip-trunking.md">Lync Server 2013 中的分支網站 SIP 主幹連線</a>＞。</td>
</tr>
</tbody>
</table>


## 支援的 SIP 主幹連線類型

Lync Server 支援 SIP 主幹使用下列連線類型：

  - Multiprotocol Label Switching (MPLS) 是可將資料從一個網路節點導向及承載到另一個網路節點的私人網路。MPLS 網路的頻寬會與其他訂戶共用，並且會為每個資料封包指派一個標籤，用以區別不同訂戶的資料。此連線類型不需要虛擬私人網路 (VPN)。可能的缺點是，過多的 IP 流量可能會干擾 VoIP 作業，除非 VoIP 流量享有優先權。

  - 不含其他流量的私人連線 (例如租用的光纖連線或 T1 線路) 通常會是最可靠而安全的連線類型。此連線類型可提供最高的通話承載能力，但通常也最昂貴。此連線類型不需要 VPN。私人連線適用於通話量大或安全性與可用性需求很高的組織。

  - 網際網路是最經濟的連線類型，但可靠性也最低。網際網路連線是唯一需要 VPN 的 Lync Server SIP 主幹連線類型。

## 選取連線類型

您的企業最適合使用的 SIP 主幹連線類型，端視您的需求與預算而定。

  - 對中型或較大的企業而言，MPLS 網路通常能提供最大的效益。它可以低於特殊私人網路的費率提供所需的頻寬。

  - 大型企業可能需要私人光纖連線、T1、T3 或更高階的連線 (歐盟地區為 E1、E3 或更高階連線)。

  - 若是小型企業或通話量低的 分支網站，使用網際網路的 SIP 主幹應是最佳選擇。不建議中型或較大的網站使用此連線類型。

## 頻寬需求

您的實作所需的頻寬量，取決於您的話務量 (您必須能夠支援的並行通話數量)。您必須將頻寬可用性納入考量，以充分使用您花錢購買的最大容量。您可以使用下列公式計算 SIP 主幹的最大頻寬需求：

SIP 主幹最大頻寬 = 同時通話數上限 x (64 kbps + 標頭大小)

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>標頭大小上限為 20 個位元組。</td>
</tr>
</tbody>
</table>


## 轉碼器支援

Lync Server 2013 僅支援下列轉碼器：

  - G.711 a-law (主要使用於北美以外的地區)

  - G.711 μ-law (使用於北美地區)

## 網際網路電話語音服務提供者

SIP 主幹連線之服務提供者端的實作方式，會根據 ITSP 而不同。如需部署資訊，請連絡服務提供者。如需已認證 SIP 主幹服務提供者的清單，請參閱＜ [Microsoft Unified Communications Open Interoperability Program 網站](http://go.microsoft.com/fwlink/?linkid=287029)＞(英文)。

如需 Microsoft 認證 SIP 主幹提供者的詳細資訊，請連絡 Microsoft 代表。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須使用 Microsoft 認證服務提供者，以確定 ITSP 支援所有周遊 SIP 主幹的功能 (例如，設定和管理工作階段，以及支援所有延伸的 VoIP 服務)。Microsoft 技術支援未延伸至使用非認證提供者的設定。如果您目前使用未獲得 SIP 主幹認證的網際網路服務提供者，則可以選擇繼續使用該提供者做為 ISP，並使用 Microsoft 認證的提供者進行 SIP 主幹作業。</td>
</tr>
</tbody>
</table>

