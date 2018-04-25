---
title: Lync Server 2013：中繼伺服器的部署指導方針
TOCTitle: 中繼伺服器的部署指導方針
ms:assetid: 7cc22b87-18d9-45e6-8402-015abd20f2e5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398622(v=OCS.15)
ms:contentKeyID: 49291430
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的中繼伺服器的部署指導方針

 

_**上次修改主題的時間：** 2012-10-12_

本主題將說明關於 中繼伺服器部署的一些規劃指導方針。在檢閱這些指導方針後，建議您使用 規劃工具建立及檢視可行的替代拓撲，作為決定最後要部署之確切拓撲的雛型。

## 要使用組合式還是獨立式 中繼伺服器？

中繼伺服器依預設會組合於中央網站上的 Standard Edition 伺服器或 前端集區中的 前端伺服器。可處理的公用交換電話網路 (PSTN) 電話數以及集區中所需的電腦數，將取決下列項目：

  - 中繼伺服器集區所控制的閘道對等數

  - 通過這些閘道的大量流量期間

  - 媒體略過 中繼伺服器的電話百分比

進行規劃時，請務必在針對非媒體旁路 PSTN 電話與 A/V 會議伺服器考量相關處理需求後，確定還有足夠能力可對於需要支援的尖峰時段電話數處理訊號互動。如果沒有足夠的 CPU，您就必須部署獨立式 中繼伺服器集區，並將 PSTN 閘道、IP-PBX 和 SBC 切割給多個子網路，而這些子網路會由一個集區中的組合式 中繼伺服器以及一或多個獨立式集區中的獨立式 中繼伺服器控制。

如果您部署的 PSTN 閘道、IP-PBX 或工作階段界限控制器 (SBC) 不支援與 中繼伺服器集區正確互動，則這些項目必須與只含單一 中繼伺服器的獨立式集區產生關聯：

  - 在集區中的 中繼伺服器之間執行網路層網域名稱系 (DNS) 負載平衡 (否則統一將流量路由傳送給集區中的所有 中繼伺服器)

  - 接受來自集區中任何 中繼伺服器的流量

您可以使用 Microsoft Lync Server 2013 規劃工具評估將中繼伺服器組合到某個前端集區時，前端集區是否可處理這些負載。如果環境無法符合這些需求，則您必須部署獨立的 中繼伺服器集區。

## 中央網站與分支網站的考量事項

中央網站上的 中繼伺服器可用來路由分支網站上 IP-PBX 或 PSTN 閘道的電話。但如果您部署 SIP 主幹，則必須在每個主幹終止的網站上部署 中繼伺服器。若要讓中央網站上的 中繼伺服器路由分支網站上 IP-PBX 或 PSTN 閘道的電話，並不需要使用媒體旁路。但是可以啟用媒體旁路的話又不同了，啟用媒體旁路將可減少媒體路徑延遲的情況，進而改善媒體品質，因為這時媒體路徑已不需遵循訊號路徑。媒體旁路也可減少集區上的處理負載。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>媒體旁路不會與每個 PSTN 閘道、IP-PBX 以及 SBC 相互溝通。Microsoft 已經與認證的合作夥伴測試了一組 PSTN 閘道和 SBC，並用 Cisco IP-PBX 完成部分測試。只有列在 Unified Communications Open Interoperability Program – Lync Server 中的產品和版本支援媒體旁路，網址為：<a href="http://go.microsoft.com/fwlink/p/?linkid=268730">http://go.microsoft.com/fwlink/p/?LinkId=268730</a>。</td>
</tr>
</tbody>
</table>


如果需要分支網站恢復能力，則必須在分支網站上部署 Survivable Branch Appliance，或部署 前端伺服器、 中繼伺服器和閘道的組合(分支網站恢復能力背後的假設是，網站上的顯示狀態和會議功能是無法恢復的)。如需關於分支網站語音功能規劃的指導方針，請參閱＜ [在 Lync Server 2013 中規劃分支網站語音彈性](lync-server-2013-planning-for-branch-site-voice-resiliency.md)＞。

就與 IP-PBX 的互動而言，如果 IP-PBX 無法正確支援具備多個早期對話的早期媒體互動與 RFC 3960 互動，則從 IP-PBX 傳送到 Lync 端點的來電可能會被截去第一聲問候語。如果中央網站上的 中繼伺服器是為其整條路由是終止於分支網站的 IP-PBX 來路由電話，前述行為可能會更嚴重，因為需要更多時間來完成訊號。如果您發現此行為，則降低聽不到第一聲問候語的唯一方法，就是在分支網站部署 中繼伺服器。

最後，如果您的中央網站上有 TDM PBX，或是您的 IP-PBX 非得使用 PSTN 閘道不可，則您必須在連接 中繼伺服器與 PBX 的電話路由上部署閘道。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要提升獨立式 Mediation Server 的媒體效能，您應該在這些伺服器上的網路介面卡啟用接收端調整 (RSS)。RSS 可讓伺服器上的多個處理器平行處理連入封包。如需詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=268731%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268731&amp;clcid=0x404</a> 的「Windows Server 的接收端調整加強」。如需如何啟用 RSS 的詳細資訊，請參閱網路介面卡文件。</td>
</tr>
</tbody>
</table>

