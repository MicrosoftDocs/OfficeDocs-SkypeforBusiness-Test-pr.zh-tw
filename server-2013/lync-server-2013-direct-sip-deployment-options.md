---
title: Lync Server 2013：SIP 直接部署選項
TOCTitle: SIP 直接部署選項
ms:assetid: 84691944-03f2-4a89-9f2b-1ab3d7f388cc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398672(v=OCS.15)
ms:contentKeyID: 49291531
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 SIP 直接部署選項

 

_**上次修改主題的時間：** 2015-03-09_

本主題提供部署直接 SIP 連線的範例拓撲。

## Lync Server 獨立

如果您的組織使用本節所述的其中一種部署， Lync Server 2013 就可以做為部分或全體組織的唯一電話語音解決方案。本節詳細說明下列部署：

  - **漸進式部署：**此選項假設您已經有專用交換機 (PBX) 基礎結構，而且打算以漸進方式將 企業語音引進組織內較小的群組或小組中。

  - **Lync Server 僅限 VoIP 部署：**此選項假設您考慮在沒有傳統電話語音基礎結構的據點上部署 企業語音。

## 漸進式部署

在漸進式部署中， Lync Server 2013 是個別小組或部門的唯一電話語音解決方案，而組織中其餘的使用者仍繼續使用 PBX。這種漸進式部署策略可讓您透過受控制的試驗計劃將 IP 電話語音引進企業。最能夠由 Microsoft Unified Communications 滿足通訊需求的工作群組，都可以移轉至 企業語音上，而其他使用者則可繼續使用現有的 PBX。您可以視需要，將其他工作群組移轉至 企業語音。

如果使用者群組已經清楚定義，有共同的通訊需求，而且願意受到集中管理，我們建議您採用漸進式選項。如果小組或部門散佈在廣大地域，這個選項也很有效，因為可以節省可觀的長途電話費。事實上，如果虛擬小組的成員可能分散在全球各地，這個選項對於建立這種虛擬小組也很實用。您可以建立、修改或解散這類小組，以快速回應不斷變化的商務需求。

下圖顯示將 企業語音 部署在 PBX 後方的一般拓撲。這是漸進式部署的建議拓撲。

**漸進式部署選項**

![部門的移轉選項圖表](images/Gg398672.e951ecf4-7cd2-425a-9106-76977492d682(OCS.15).jpg "部門的移轉選項圖表")

> [!NOTE]  
> 如果您要使 Lync Server 部署和取得認證的直接 SIP 協力廠商連線， 中繼伺服器和 PBX 之間便不需要公用交換電話網路 (PSTN) 閘道。如需取得認證的直接 SIP 協力廠商清單，請參閱 Microsoft Unified Communications Open Interoperability Program 網站 ( <a href="http://go.microsoft.com/fwlink/?linkid=203309%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=203309&amp;clcid=0x404</a>)。



> [!NOTE]  
> 此圖表展示的媒體路徑已啟用媒體旁路 (建議設定)。如果您選擇停用媒體旁路，媒體路徑將經由 中繼伺服器 路由傳送。



在此拓撲中，選取的部門或工作群組已啟用 企業語音。PSTN 閘道會將啟用 Voice over Internet Protocol (VoIP) 的工作群組連結至 PBX。啟用 企業語音的使用者 (包括遠端工作者) 會透過 IP 網路通訊。 企業語音使用者向 PSTN 和未啟用 企業語音的同事所撥打的電話，都會路由傳送至適當的 PSTN 閘道。來自仍位於 PBX 系統上之同事，或者來自 PSTN 上之來電者的通話，會路由傳送至 PSTN 閘道，閘道會將通話轉送至 Lync Server 以便路由傳送。

若要連接 企業語音 與現有的 PBX 基礎結構以便達成互通的目的，有兩種建議採用的設定： 企業語音 在 PBX 後方以及 企業語音 在 PBX 前方。

## Enterprise Voice 在 PBX 後方

將 企業語音 部署於 PBX 後方時，所有來自 PSTN 的通話都會送達 PBX，而 PBX 會將 企業語音 使用者的通話路由傳送至 PSTN 閘道，將 PBX 使用者的通話路由傳送至 PBX。

## Enterprise Voice 在 PBX 前方

將 企業語音 部署於 PBX 前方時，所有通話都會送達 PSTN 閘道，而閘道會將 企業語音 使用者的通話路由傳送至 Lync Server，將 PBX 使用者的通話路由傳送至 PBX。從 企業語音 和 PBX 使用者撥給 PSTN 的通話，都會透過 IP 網路路由傳送到最具成本效益的 PSTN 閘道。下表說明此設定的優點和缺點。

### 將 企業語音部署在 PBX 前方的優點和缺點

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>優點</th>
<th>缺點</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PBX 仍然會服務未啟用 企業語音 的使用者。</p></td>
<td><p>現有的閘道可能無法支援所需的功能或容量。</p></td>
</tr>
<tr class="even">
<td><p>PBX 可處理所有舊版的裝置。</p></td>
<td><p>需有從閘道到 PBX 以及從閘道到 中繼伺服器 的主幹。服務提供者需提供較多主幹。</p></td>
</tr>
<tr class="odd">
<td><p>企業語音 使用者可保留相同的電話號碼。</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


## Lync Server 僅限 VoIP 部署

企業語音也可以為新的企業和現有企業的新辦公室，提供一個實作全功能 VoIP 解決方案的機會，而且不必擔心 PBX 的整合或是部署與維護 IP-PBX 基礎結構的昂貴成本。這個解決方案同時支援位於據點現場和遠端的工作者。

在此部署中，所有的通話都會透過 IP 網路路由傳送。撥給 PSTN 的通話會路由傳送至適當的 PSTN 閘道。 Lync 2013 或 Lync Phone Edition 都可以當做軟體電話來使用。無法使用遠端呼叫控制而且也不需要，因為 PBX 電話已不存在，所以使用者不需要控制。您可以透過 Exchange 整合通訊 (UM) 的選用部署，來提供語音信箱和自動語音應答服務。

> [!NOTE]  
> 除了支援 Lync Server 2013 所需的網路基礎結構以外，僅限 VoIP 部署還能使用小型的合格閘道來支援傳真機和類比裝置。



下圖說明僅限 VoIP 部署的一般拓撲。

**僅限 VoIP 部署選項**

![Greenfidle 部署選項](images/Gg398672.820dc5fe-0e20-431b-ae4e-fefdf2221d3b(OCS.15).jpg "Greenfidle 部署選項")

> [!NOTE]  
> 此圖表展示的媒體路徑已啟用媒體旁路 (建議設定)。如果您選擇停用媒體旁路，媒體路徑將經由 中繼伺服器 路由傳送。


