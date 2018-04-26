---
title: 針對具有多個資料中心的大型組織提供的 Lync Server 2013 參考拓撲
TOCTitle: 具有多個資料中心的大型組織的參考拓撲
ms:assetid: 9a6aeae6-629b-49e6-9804-7ef369d7c3dc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398797(v=OCS.15)
ms:contentKeyID: 49291788
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 具有多個資料中心的大型組織中的 Lync Server 2013 參考拓撲

 

_**上次修改主題的時間：** 2012-10-22_

任何規模的組織只要具有一個以上的中央網站，都適合使用含有多個資料中心的大型組織參考拓撲。下圖中的確切拓撲是用於擁有 50,000 位使用者的組織，其中 20,000 位使用者在中央網站 A，20,000 位在中央網站 B，以及 10,000 位在中央網站 C 和分支網站。此圖所示的拓撲類型適用於任何使用者數量的組織。

除了 前端伺服器集區提供的高可用性，此拓撲還加上災害復原支援。中央網站 A 與 B 的 前端集區會配對在一起。如果其中一個集區停機，系統管理員可以為受影響的使用者將服務切換至未受影響網站上的所配對集區。

此拓撲將以多張圖表示，第一張圖是概觀，接下來則是各中央網站的詳細檢視。

**含有多個資料中心的大型組織參考拓撲的概觀**

![多個資料中心的參考拓撲](images/Gg398797.471e1ce9-be11-44b9-9f4a-59e0551b7b30(OCS.15).jpg "多個資料中心的參考拓撲")

**大型組織的參考拓撲：中央網站 A 的詳細檢視**

![規劃參考拓撲 A](images/Gg398797.dab33f19-e77b-42da-9047-858fb9851264(OCS.15).jpg "規劃參考拓撲 A")

**大型組織的參考拓撲：中央網站 B 的詳細檢視**

![規劃參考拓撲 B](images/Gg398797.5ccaf1d4-bd53-4cb7-96fe-723147334e7f(OCS.15).jpg "規劃參考拓撲 B")

**大型組織的參考拓撲：中央網站 C 的詳細檢視**

![規劃參考拓撲 C](images/Gg398797.7238ca40-340c-491f-b497-ddc2665dadb6(OCS.15).jpg "規劃參考拓撲 C")

  - **前端集區互相配對以便進行災害復原。**   網站 A 與網站 B 上的 前端集區 會互相配對以提供災害復原支援。如果其中一個網站上的集區失敗，系統管理員可以將使用者從該網站容錯移轉至另一個網站上的所配對 前端集區，讓使用者受到的服務中斷減至最低。這兩個前端集區各自具有 6 部伺服器，足以在容錯移轉時應付兩個集區的所有 40,000 個使用者。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中規劃高可用性和災害復原](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)＞。

  - **後端伺服器互相鏡像**   為了讓基本的使用者功能有更高的可用性，這家組織為每個 前端集區都部署了一對鏡像的 後端伺服器。這是選用拓撲，您可以改為選擇部署單一 後端伺服器。

  - **在分支網站使用 Standard Edition。**此組織將網站 C 視為分支網站，因為它只有 600 位員工。不過，使用者之間可能有許多 A/V 會議。如果將該網站部署在 Lync Server 中作為分支網站，則這些會議的媒體會穿越廣域網路 (WAN)，往返於已部署前端伺服器的中央網站。為了避免這種潛在的頻寬負載，組織在此網站安裝了一對 Standard Edition 伺服器來裝載這些會議。因為此處安裝了 Standard Edition，所以 Lync Server 依定義會將它視為中央網站，而在 拓撲產生器和 規劃工具中也會如此看待它。
    
    只要一部 Standard Edition 伺服器就足以應付這裡所需的效能，但是這家組織部署了兩部伺服器並且將它們互相配對，以防萬一其中一部伺服器停機，仍然可以提供高可用性。
    
    雖然網站 C 會視為中央網站，但您不必在此網站部署 Edge Server。在此範例中，網站 C 會使用網站 A 上部署的 Edge Server。

  - **監控和封存**   此組織已部署監控和封存。當您部署監控或封存時，它會在每一部前端伺服器上執行。這些功能的資料庫可以與後端資料庫位於相同的伺服器，或位於不同伺服器。此組織已將這些資料庫置於不同於後端伺服器的伺服器上 (位於網站 C 中)。這裡的資料庫會從所有網站中的前端伺服器接收監控和封存資料。

  - **分支網站部署選項。**此組織實際具有超過 50 個分支網站，其中只有 3 個顯示在詳細圖表中。分支網站 1 和 3 沒有可恢復的 WAN 連結來連到中央網站，因此，為防萬一與中央網站的 WAN 連結中斷，它們部署了 Survivable Branch Appliance 來提供電話服務。不過，分支網站 2 具有可恢復的 WAN 連結，因此只需要有公用交換電話網路 (PSTN) 閘道。那裡部署的 PSTN 閘道可支援媒體旁路，所以分支網站 B 不需要有中繼伺服器。如需關於決定要在分支網站安裝哪些項目的詳細資訊，請參閱規劃文件中的 [在 Lync Server 2013 中規劃企業語音復原](lync-server-2013-planning-for-enterprise-voice-resiliency.md)。

  - **SIP 主幹連線和中繼伺服器。**請注意，在中央網站 B，中繼伺服器並未與前端伺服器位於同一部伺服器。這是因為在使用 SIP 主幹的網站上，建議使用獨立的中繼伺服器。在其他大多數情況下，還是建議您將中繼伺服器與前端伺服器置於同一部伺服器。如需關於中繼伺服器拓撲的詳細資訊，請參閱規劃文件中的 [Lync Server 2013 中之中繼伺服器的元件和拓撲](lync-server-2013-components-and-topologies-for-mediation-server.md)。

  - **已部署常設聊天室。**   此組織已部署必要的伺服器以啟用「常設聊天室」。其部署了多個常設聊天室前端伺服器以處理集區中的使用者數目帶來的負載，以及提供高可用性。其也部署了常設聊天室的規範，並且將常設聊天室存放區和常設聊天室規範存放區分開置於不同的伺服器上。這些存放區可以置於相同的伺服器上，甚至可以置於與後端伺服器相同的伺服器上，但是此組織選擇將它們分開存放以提供更佳的效能。

  - **DNS 負載平衡。**前端集區和 Edge Server 集區。如此一來，就不需要對 Edge Server 的內部介面使用硬體負載平衡器，大幅減少您必須花在為其餘集區安裝和維護硬體負載平衡器的時間，因為只有 HTTP 流量才需要硬體負載平衡器。如需關於 DNS 負載平衡的詳細資訊，請參閱規劃文件中的 [Lync Server 2013 中的 DNS 負載平衡](lync-server-2013-dns-load-balancing.md)。

  - **Exchange UM 部署。**Lync Server 可搭配「內部部署」 的 Exchange 整合通訊 (UM) ，也可搭配「託管式」 Exchange UM。中央網站 A 包含的 Exchange 整合通訊 (UM) Server 是執行 Microsoft Exchange Server，而非 Lync Server。 Lync Server 的 Exchange UM 功能是在前端集區上執行。
    
    中央網站 B 使用託管式 Exchange，所以也會裝載 Exchange UM Server 功能。
    
    如需 Exchange UM 的詳細資訊，請參閱規劃文件中的＜ [在 Lync Server 2013 中規劃 Exchange Unified Messaging 整合](lync-server-2013-planning-for-exchange-unified-messaging-integration.md)＞及＜ [Lync Server 2013 中的主控 Exchange 整合通訊整合](lync-server-2013-hosted-exchange-unified-messaging-integration.md)＞。

  - **Office Web Apps Server。** 建議您在每個使用 Web 會議的組織中部署 Office Web Apps Server 或 Office Web Apps Server 陣列。您可以在某個網站中部署單一 Office Web Apps Server 陣列，為來自所有網站的流量提供服務，或者在每個網站中部署。Office Web Apps Server 讓 Powerpoint 投影片可以在 Web 會議中呈現。如需詳細資訊，請參閱＜ [設定 Office Web Apps Server 與 Lync Server 2013 的整合](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md)＞。

  - **可以新增 Director。** 如果此組織想要提升對於拒絕服務攻擊的安全性，也可以部署 Director 集區。 Director 是 Lync Server 中獨立、選用的伺服器角色，不裝載使用者帳戶，也不提供目前狀態或會議服務。它的功能是擔任下一個內部躍點伺服器， Edge Server 會將目的地為內部伺服器的輸入 SIP 流量先路由給它。 Director 會預先驗證傳入的要求，再將要求重新導向至使用者的主集區或伺服器。在 Director 進行預先驗證，將能夠先捨棄掉來自部署所不認識之使用者帳戶的要求。 Director 可協助前端伺服器隔絕掉惡意的流量，例如拒絕服務 (DoS) 攻擊。如果網路上有此類攻擊產生的無效外部流量大量流竄，這些流量會終止於 Director。

  - **已部署 System Center Operations Manager。** 建議您監控 Lync Server 部署的健康情況，以確保服務對使用者而言時時可用。您可以使用 System Center Operations Manager Management Pack for Lync 監控 Lync，該工具可以從 Microsoft 免費下載。使用 Lync Management Pack，您可以在問題發生時主動取得即時警示、執行綜合交易以測試端對端 Lync 功能、取得服務可用性報告等等。這可以協助您在部署的使用者遇到問題之前主動回應。
    
    此組織已分別在每個中央網站部署一個 System Center Operations Manager 伺服器。

