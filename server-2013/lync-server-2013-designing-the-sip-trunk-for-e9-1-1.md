---
title: Lync Server 2013：為 E9-1-1 設計 SIP 主幹
TOCTitle: 為 E9-1-1 設計 SIP 主幹
ms:assetid: 4f93b974-b460-45c7-a4a8-6f38e34840f5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398323(v=OCS.15)
ms:contentKeyID: 49290887
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中為 E9-1-1 設計 SIP 主幹

 

_**上次修改主題的時間：** 2012-10-03_

Lync Server 使用 SIP 主幹，將緊急通話連接至 E9-1-1 服務提供者。您可以在一個中央網台、多個中央網台或每個分支網站上設定 E9-1-1 的緊急服務 SIP 主幹。不過，如果來電者網站與主控緊急服務 SIP 主幹的網站之間的 WAN 連結無法使用，由中斷連線網站上的使用者所撥打的電話在使用者語音原則中，需要有特殊的電話使用方式記錄來指定透過本機公用交換電話網路 (PSTN) 閘道，將電話路由至 ECRC。如果通話許可控制並行通話限制有效，則有同樣的需求。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有兩種方法可以在 Lync Server 環境中實作 SIP 主幹：
<ul>
<li><p>使用多重主目錄 中繼伺服器，利用它們向外公開路由的介面與 SIP 主幹提供者通訊。</p></li>
<li><p>使用內部部署工作階段邊界控制器 (SBC) 在 中繼伺服器和 SIP 主幹提供者的服務之間提供安全的分割點。</p></li>
</ul>
如果您選擇後者，請確定您所選擇的 SBC 品牌與型號已取得認證，並且支援傳遞「目前狀態資訊資料格式位置物件」(PIDF-LO) 位置資料做為其 SIP INVITE 的一部分。否則電話將會送達去除其位置資訊的緊急服務服務提供者。如需有關認證的 SBC 的詳細資訊，請參閱＜Microsoft Lync 適用的基礎結構＞，網址為： <a href="http://go.microsoft.com/fwlink/?linkid=248425%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=248425&amp;clcid=0x404</a>。<br />
E9-1-1 服務提供者為您提供一組 SBC 的存取做為後備之用。您必須做幾項有關 中繼伺服器拓樸及通話路由設定的決定。您是要將兩台 SBC 視為對等，並對它們之間的通話使用循環配置資源路由；或是要將一個 SBC 指派為主要，而另一個指派為次要呢？</td>
</tr>
</tbody>
</table>


如需有關在 Lync Server 中部署 SIP 主幹的詳細資訊，請參閱＜ [如何在 Lync Server 2013 中實作 SIP 主幹？](lync-server-2013-how-do-i-implement-sip-trunking.md)＞。為了協助決定如何部署 E9-1-1 的 SIP 主幹，您應該先回答下列問題。

  - **您應該在專用的租用網際網路連線上還是共用的網際網路連線上部署 SIP 主幹？**  
    重點是一定要能夠接通緊急通話。專用線路可提供不被網路上其他流量佔用的連線，並讓您能夠實作服務品質 (QoS)。請記住，如果您透過公用網際網路連線至緊急服務服務提供者，而且需要保證緊急電話的機密性，則需要 IPSec 加密。

<!-- end list -->

  - **您的 E9-1-1 部署是否具有災難容錯設計？**  
    因為這是緊急解決方案，所以恢復能力很重要。請將您的主要和次要 中繼伺服器及 SIP 主幹部署於具有災難容錯能力的地點。您可以將主要 中繼伺服器盡量部署於接近其所支援的使用者附近，同時利用次要 中繼伺服器 (位於不同地理位置) 來路由容錯移轉的通話。

<!-- end list -->

  - **您是否應該為每個分公司部署個別的 SIP 主幹？**  
    Lync Server 提供了幾項用以處理分公司語音恢復能力的策略，包括：佈建可恢復的資料網路、在每個分公司部署 SIP 主幹，或是在 WAN 中斷期間將電話向外發送至區域閘道。如需詳細資訊，請參閱＜ [Lync Server 2013 中的分支網站 SIP 主幹連線](lync-server-2013-branch-site-sip-trunking.md)＞。

<!-- end list -->

  - **是否啟用通話許可控制 (CAC)?**  
    Lync Server 處理緊急通話的方式與處理一般通話沒有任何不同。因此，頻寬管理或通話許可控制 (CAC) 可能對 E9-1-1 組態有負面影響。如果啟用 CAC，且在路由緊急通話的連結上的流量超出設定的限制，則緊急通話可能會被封鎖或路由至本機 PSTN 閘道。如同本主題稍早所述，這類通話將會沒有位置資料，並且必須以手動方式路由至 ECRC。

