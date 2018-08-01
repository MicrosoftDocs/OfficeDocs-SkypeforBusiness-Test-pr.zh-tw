---
title: Lync Server 2013 適用於中型組織的參考拓樸
TOCTitle: 適用於中型組織的參考拓樸
ms:assetid: 446b0914-2198-445e-ab6e-94802acebd5c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425939(v=OCS.15)
ms:contentKeyID: 49290760
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 中型組織內 Lync Server 2013 的參考拓樸

 

_**上次修改主題的時間：** 2013-10-07_

具有高可用性和單一資料中心的參考拓撲是專為具有一個中央網站的中小型組織所設計。下圖的確切拓撲適用於具有 20,000 位使用者的組織。

**適用於中型組織的參考拓樸**

![單一資料中心圖表的參考拓撲](images/Gg425939.12b574fd-0b14-4563-a88c-3c8b0809bb90(OCS.15).jpg "單一資料中心圖表的參考拓撲")

  - **新增更多前端伺服器來容納更多使用者。** 此圖的確切拓撲有三部前端伺服器，以支援 20,000 位使用者。如果您只有單一中央網站，但有更多使用者，您只要將更多前端伺服器新增至集區即可。以十二部前端伺服器為例，每個集區的使用者數目上限為 80,000。
    
    不過，如果網站再新增一個前端集區，則單一個網站拓撲可以支援更多使用者。

  - **可以新增災害復原。** 對於這個組織，他們的 Lync Server 服務的高可用性是必要的功能，但災害復原並不是。他們所部署的 前端伺服器的集區提供高可用性。
    
    如果他們想要新增災害復原能力，可以考慮建立另一個資料中心，並在其中新增另一個前端集區，然後與他們目前資料中心內的前端集區進行配對。接下來，如果有影響其主要集區的災害，系統管理員就可以將使用者容錯移轉至備用集區。

  - **後端伺服器鏡像。**為了替基本使用者功能提供更多高可用性，組織為每個 前端集區部署了一組 後端伺服器的鏡像配對。這是 Lync Server 2013 的新拓樸選項 (選用)。您也可以改為選擇部署單一 後端伺服器。

  - **監控伺服器資料庫選項。** 這個組織部署了監控，以確保 Enterprise Voice 電話和 A/V 會議的品質。每部前端伺服器上都部署了監控，而監控資料庫會與後端伺服器組合在一起。我們也支援有監控資料庫位於另一部伺服器上的拓樸。

  - **Edge Server 高可用性。** 在具有 20,000 位使用者的這個範例組織中，只要一部 Edge Server 就有足夠的效能。不過，在集區中部署兩部伺服器可以提供高可用性。

  - **分支網站部署選項。** 此拓撲中的組織部署了 Enterprise Voice 作為語音解決方案。分支網站 1 沒有彈性的廣域網路 (WAN) 連結來連到中央網站，因此，為防萬一與中央網站的 WAN 連結中斷，它部署了 Survivable Branch Appliance 來維護許多 Lync Server 功能。不過，分支網站 2 具有彈性的 WAN 連結，因此只需要有公用交換電話網路 (PSTN) 閘道。此網站部署的 PSTN 閘道支援媒體旁路，所以分支網站 2 不需要有中繼伺服器。如需決定要在分支網站部署哪些項目的詳細資訊，請參閱規劃文件中的 [在 Lync Server 2013 中規劃分支網站語音彈性](lync-server-2013-planning-for-branch-site-voice-resiliency.md)＞

  - **DNS 負載平衡。** 前端集區和 Edge Server 集區部署了 SIP 流量的 DNS 負載平衡。如此一來，Edge Server 就不需要硬體負載平衡器，這樣可大幅減少為其他集區安裝和維護硬體負載平衡器的工作，因為只有 HTTP 流量才需要硬體負載平衡器。如需 DNS 負載平衡的詳細資訊，請參閱規劃文件中的 [Lync Server 2013 中的 DNS 負載平衡](lync-server-2013-dns-load-balancing.md)。

  - **Exchange UM 部署。** 此參考拓撲包含的 Exchange 整合通訊 (UM) Server 是執行 Microsoft Exchange Server，而非 Lync Server。
    
    如需 Exchange UM 的詳細資訊，請參閱規劃文件中的＜ [在 Lync Server 2013 中規劃 Exchange Unified Messaging 整合](lync-server-2013-planning-for-exchange-unified-messaging-integration.md)＞及＜ [Lync Server 2013 中的主控 Exchange 整合通訊整合](lync-server-2013-hosted-exchange-unified-messaging-integration.md)＞。

  - **Office Web Apps Server。** 我們建議在使用 Web 會議的每個組織中都部署 Office Web Apps Server 或 Office Web Apps Server 陣列。Office Web Apps Server 讓 Powerpoint 投影片可能可以在 Web 會議中播放。如需詳細資訊，請參閱＜ [設定 Office Web Apps Server 與 Lync Server 2013 的整合](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md)＞。

  - **建議使用 Edge Server。** Edge Server 雖然不是必須部署的項目，但仍建議在任何規模的部署使用它。您可以部署 Edge Server 以對目前在組織防火牆外的使用者提供服務，進而發揮最大的 Lync Server 投資效益。包含下列優勢：
    
      - 貴組織本身的使用者在家工作或在出差時仍可使用 Lync Server 功能。
    
      - 您的使用者可以邀請外部使用者參與會議。
    
      - 如果您的合作夥伴、廠商或客戶組織也使用 Lync Server，則可以與該組織構成「同盟關係」 。然後您的 Lync Server 部署會辨識來自該同盟組織的使用者，進而產生更好的合作成果。
    
      - 您的使用者可以和下列公用 IM 服務的使用者交換立即訊息：Windows Live、AOL、Yahoo\! 及 Google Talk。與這些服務的公用 IM 連線可能需要個別的授權。
        
        > [!IMPORTANT]  
		> <ul>
        > <li><p>自 2012 年 9 月 1 日起，Microsoft Lync 公用 IM 連線使用者訂閱授權 (&quot;PIC USL&quot;) 無法再以新合約或續約的方式購買。持有使用中授權的客戶將可繼續與 Yahoo! Messenger 維持同盟關係直至服務終止日。目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的結束日期。如需詳細資訊，請參閱 <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>。</p></li>
        > <li><p>PIC USL 是針對每位使用者的每月訂閱授權，為 Lync Server 或 Office Communications Server 與 Yahoo! Messenger 同盟的必要授權。Microsoft 是否提供此項服務視 Yahoo! 的支援而定，而此基礎合約將告結束。</p></li>
        > <li><p>更勝以往，Lync 成為連接全世界組織之間以及個人之間的強大工具。除了 Lync Standard CAL 之外，與 Windows Live Messenger 同盟不需要其他使用者/裝置授權。此清單更將加入 Skype 同盟，讓 Lync 使用者可透過 IM 和語音觸及數億位使用者。</p></li>
        > </ul>

  - **可以新增 Director。** 如果這個組織想要協助提高針對拒絕服務攻擊的安全性，也可以部署 Director 的集區。 Director 在不裝載使用者帳戶或是提供目前狀態或會議服務的 Lync Server 中，是個別的選用伺服器角色，其作為內部的下一個躍點伺服器，讓 Edge Server 將預定要進入內部伺服器的輸入 SIP 流量路由至該處。 Director 會預先驗證輸入要求，並將其重新導向至使用者的主集區或伺服器。Director 的預先驗證允許捨棄部署無法辨識的使用者帳戶的要求。 Director 有助於隔絕前端伺服器的惡意流量，例如拒絕服務 (DoS) 攻擊。如果網路上因此類攻擊而充斥無效的外部流量，這些流量將止於 Director。

  - **建議使用 System Center Operations Manager。** 我們建議您監控 Lync Server 部署的狀況，協助確保一般使用者的服務可用性。您可以從 Microsoft 下載免費的 System Center Operations Manager Management Pack for Lync，用以監控 Lync。使用 Lync Management Pack 可讓您在問題發生時主動獲得即時警示、執行綜合交易以測試端對端 Lync 功能、取得服務可用性的報告等等。如此有助您在一般使用者遇到問題之前，就先透過您的部署主動回應這些問題。

