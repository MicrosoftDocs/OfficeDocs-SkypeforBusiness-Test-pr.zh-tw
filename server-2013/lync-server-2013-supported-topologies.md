---
title: Lync Server 2013 支援的拓撲
TOCTitle: 支援的拓撲
ms:assetid: 3475d430-0394-491b-a09b-ba85bd62be70
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425833(v=OCS.15)
ms:contentKeyID: 49290548
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中支援的拓撲

 

_**上次修改主題的時間：** 2014-01-14_

Lync Server 2013 支援在組織內部部署的網站部署，以及將內部部署與 商務用 Skype Online 部署整合，這稱為混合部署。在混合部署中，一些使用者會位於內部部署，而一些使用者會位於線上。

針對內部部署， Lync Server 2013 支援部署一或多個可調整以達到高度可用性與位置需求的站台。您可以建構這些站台及其元件，以達到組織在存取與恢復能力方面的需求。

Lync Server 2013 內部部署包含下列各項：

  - 部署中至少要有一個中央站台 (也稱為資料中心)。每個中央站台都至少要有一個 Enterprise Edition 前端集區或一部 Standard Edition Server。這些項目包含：
    
      - Enterprise Edition 前端集區包含一或多個前端伺服器 (通常至少兩個前端伺服器，以維持延展性)，以及一個獨立的後端伺服器。前端集區最多可包含十二個前端伺服器。多個前端伺服器必須有負載平衡。針對 SIP 流量，建議使用 DNS 負載平衡，但也支援硬體負載平衡。如果您針對 SIP 流量使用 DNS 負載平衡，仍需要針對 HTTP 流量使用硬體負載平衡器。若要讓資料庫保有高可用性，建議您使用 SQL Server 鏡像。後端資料庫必須要有個別的執行個體，但您可以組合封存資料庫、監控資料庫、常設聊天室資料庫，以及常設聊天室規範資料庫。 Lync Server 2013 支援在您的部署中使用共用叢集，以進行檔案共用。如需資料庫儲存需求的詳細資料，請參閱 [Lync Server 2013 中的資料庫軟體支援](lync-server-2013-database-software-support.md)。如需檔案儲存需求的詳細資訊，請參閱 [Lync Server 2013 中的檔案儲存支援](lync-server-2013-file-storage-support.md)。
        
        > [!IMPORTANT]  
        > 如果您組合 Lync Server 資料庫，則強烈建議您評估可能會影響可用性和效能的所有因素。若要確認容錯移轉功能，建議您測試所有容錯移轉狀況。
        
    
      - Standard Edition Server，其中包含組合的 SQL Server Express 資料庫。

  - 部署中也可以有一或多個與中央網站相關聯的分支網站。

本節將說明 Lync Server 2013 部署的站台與元件。如需有關 Lync Server 2013 站台、拓撲與元件規劃的詳細資訊，請參閱＜規劃＞文件中的 [規劃 Lync Server 2013 前必須知道的拓撲基本知識](lync-server-2013-topology-basics-you-must-know-before-planning.md)與 [Lync Server 2013 中的參考拓撲](lync-server-2013-reference-topologies.md)。如需有關整合舊版元件的詳細資訊，請參閱 [Lync Server 2013 中支援的移轉路徑和並存案例](lync-server-2013-supported-migration-paths-and-coexistence-scenarios.md)。

> [!NOTE]  
> 前端、Edge、中繼和 Director 伺服器角色不支援延伸的集區。



## 中央站台的拓撲與元件 (內部部署)

雖然中央站台拓撲必須包含一個前端集區或一部 Standard Edition Server，但各個中央站台也可包含下列項目：

  - 多個前端集區，可位於相同或不同的網域。但是，前端集區中的所有前端伺服器與該集區的後端伺服器必須位於相同網域。

  - 多部 Standard Edition Server。

  - Office Web Apps Server，可以搭配使用 Lync Server 2013 中的 Office Web 應用程式，來處理 Microsoft PowerPoint 簡報的共用與轉譯。

  - 您周邊網路中的 Edge Server 或 Edge 集區 (若您要讓部署支援同盟協力廠商、公用 IM 連線、Extensible Messaging and Presence Protocol (XMPP) 閘道、遠端使用者存取、匿名使用者與會功能或 Exchange 整合通訊 (UM))。Edge Server 不可與任何其他伺服器角色組合。建議在情況允許時使用 DNS 負載平衡，但也支援硬體負載平衡。內部 Edge 介面和外部 Edge 介面必須使用相同類型的負載平衡。您不能在一個 Edge 介面上使用 DNS 負載平衡，而在另一個 Edge 介面上使用硬體負載平衡。如需有關負載平衡需求與支援的詳細資訊，請參閱＜規劃＞文件中的 [在 Lync Server 2013 中規劃外部使用者存取](lync-server-2013-planning-for-external-user-access.md)，以及＜部署＞文件中的 [在 Lync Server 2013 中部署外部使用者存取](lync-server-2013-deploying-external-user-access.md)。

  - 中繼伺服器或集區 (如果您要在中央站台上的前端集區中支援企業語音或電話撥入式會議)。您可以根據企業語音支援的部署方式，在前端集區中組合中繼伺服器 (預設值)，或是部署獨立式中繼伺服器或集區。您可以使用 DNS、硬體或應用程式負載平衡 (視何者適用)，分散來自中繼伺服器集區的閘道對等 (包括 PSTN 閘道、IP-PBX 或 SIP 主幹工作階段界限控制 (SBC)) 的流量。如需有關規劃適當中繼伺服器拓撲的詳細資訊，請參閱＜規劃＞文件中的 [Lync Server 2013 中的中繼伺服器的部署指導方針](lync-server-2013-deployment-guidelines-for-mediation-server.md)。

  - 常設聊天室伺服器 (如果您想讓使用者能夠參與長期持續無間的主題式多方交談)。若要提供更多的容量以及提高可靠性，您的拓撲可以包括多部執行 常設聊天室伺服器 的電腦。您可以將 常設聊天室伺服器 與企業集區中的其他伺服器角色組合。但是，您可以在 Standard Edition Server 中組合 常設聊天室伺服器。常設聊天室需要一個資料庫，而且，如果您實作常設聊天室規範，則需要常設聊天室規範資料庫，但是資料庫可與封存資料庫或監控資料庫組合，或者在 Enterprise Edition 前端集區的後端伺服器上組合。如需有關規劃適當 常設聊天室伺服器 拓撲的詳細資訊，請參閱＜規劃＞文件中的 [在 Lync Server 2013 中規劃常設聊天室伺服器](lync-server-2013-planning-for-persistent-chat-server.md)。

  - 監控 (如果您要在部署中支援音訊/視訊經驗品質 (QoE) 的資料收集以及企業語音與 A/V 會議的詳細通話記錄 (CDR))。您可以選擇性地安裝 Microsoft System Center Operations Manager (舊名為 Microsoft Operations Manager)，它會使用監控 CDR 與 QoE 資料產生幾近即時的通知，以顯示通話穩定性與媒體品質的狀況。在部署時，監控可與前端伺服器或 Standard Edition Server 組合。監控必須要有資料庫，但此資料庫可與封存伺服器、常設聊天室資料庫、常設聊天室規範資料庫或 Enterprise Edition 前端集區的後端伺服器組合。

  - 封存 (如果您基於規範而要在部署中封存 IM 通訊與會議內容)。在部署時，封存可與前端伺服器或 Standard Edition Server 組合。封存儲存需要部署封存資料庫或與 Exchange 2013 儲存整合。如果您使用這兩者 (稱為 *「混合模式」* )， Exchange 2013 儲存可用來為位於 Exchange 2013 的使用者儲存封存資料，而封存資料庫可用來為您部署中的所有其他使用者封存資料。如果您需要封存資料庫，該資料庫可以在監控資料庫、常設聊天室資料庫、常設聊天室規範資料庫或前端集區的後端伺服器上組合。如需規劃適當封存拓撲的詳細資訊，請參閱＜規劃＞文件中的 [在 Lync Server 2013 中規劃封存](lync-server-2013-planning-for-archiving.md)。

  - Director 或 Director 集區 (如果您想促進對使用者主集區之 Lync Server 2013 使用者要求的恢復能力與重新導向性，而使用者的主集區可以是 Enterprise Edition 前端集區或 Standard Edition Server)。建議您在每個支援外部使用者存取的中央站台以及每個部署一或多個前端集區的中央站台上，部署 Director 或 Director 集區。每個 Director 集區最多可包含十個 Director。Director 不可與任何其他伺服器角色組合。如需有關規劃適當 Director 拓撲的詳細資訊，請參閱＜規劃＞文件中的 [Lync Server 2013 中的 Director 案例](lync-server-2013-scenarios-for-the-director.md)。

  - 反向 Proxy，這並不是 Lync Server 2013 元件，但若您想要支援同盟使用者共用 Web 內容或支援行動流量，就必須使用。任何 Lync Server 2013 伺服器角色皆不可與反向 Proxy 伺服器組合，但是您可以在用於其他應用程式之組織中的現有反向 Proxy 伺服器上設定支援，來實作 Lync Server 2013 部署的反向 Proxy 支援。如需有關反向 Proxy 伺服器的詳細資訊，請參閱＜部署＞文件中的 [設定 Lync Server 2013 的反向 Proxy 伺服器](lync-server-2013-setting-up-reverse-proxy-servers.md)。

> [!NOTE]  
> 在 Lync Server 2013 中，A/V 會議、監控及封存會在前端伺服器上執行，而且不再是個別的伺服器角色。



您在中央網站上部署的所有前端集區與 Standard Edition Server，將會共用您為中央網站所部署的下列各項：

  - Director 或 Director 集區

  - 獨立式中繼伺服器或集區

  - Office Web Apps Server

  - Edge Server 或 Edge 集區

  - 常設聊天室伺服器或集區

  - 監控

  - 封存

> [!NOTE]  
> 如果您想支援 Exchange 2013 Unified Messaging 的整合，您可以在 Lync Server 2013 部署中實作 Exchange UM Server，但這並不是 Lync Server 2013 站台的元件。



多個中央網站也可共用您在某個中央網站上部署的下列任何項目：

  - 獨立式中繼伺服器或集區

  - Edge Server 或 Edge 集區

  - 常設聊天室伺服器或集區

  - 封存

  - 監控

> [!NOTE]  
> Exchange UM Server 可以在您的 Lync Server 2013 部署中實作，也可以讓多個中央站台共用，但它並不是 Lync Server 2013 站台的元件。



如需有關 Lync Server 2013 伺服器角色和功能的詳細資訊，請參閱＜規劃＞文件中的 [Lync Server 2013 中的伺服器角色](lync-server-2013-server-roles.md)。

如需 Lync Server 2013 伺服器組合支援的摘要，請參閱 [Lync Server 2013 中支援的伺服器組合](lync-server-2013-supported-server-collocation.md)。

除了本節先前所討論的伺服器角色和功能， Lync Server 2013 還有其他元件與選項，其中包含下列部分或所有項目：

  - 防火牆

  - PSTN 閘道 (如果部署企業語音)

  - Exchange UM Server

  - DNS 負載平衡

  - 硬體負載平衡器

  - SQL Server 資料庫

  - 檔案共用

如需有關所有 Lync Server 2013 功能、元件及選項的詳細資訊，請參閱＜規劃＞文件。

## 分支站台的拓撲與元件 (內部部署)

分支站台會與中央站台相關聯，而且分支站台中的每個 Survivable Branch Appliance 都會與相關聯之中央站台上的一個 Enterprise Edition 前端集區或一部 Standard Edition Server 相關聯。分支站台大部分的功能皆依存於中央站台，因此分支站台上的元件僅包含下列項目：

  - 一個 Survivable Branch Appliance，其中包含具有部分 Lync Server 功能的公用交換電話網路 (PSTN) 閘道。中繼伺服器可與 Survivable Branch Appliance 上登錄器的執行個體組合，而您可以部署獨立式中繼伺服器或中繼伺服器集區。

  - Survivable Branch Server，此為已安裝 Lync Server 2013 登錄器與中繼伺服器軟體且執行 Windows Server 的伺服器。

  - 獨立式 PSTN 閘道 (不是 Survivable Branch Appliance 的一部分) 與獨立式中繼伺服器。

Survivable Branch Server 的需求與任何 Lync Server 2013 伺服器角色的需求均相同。

