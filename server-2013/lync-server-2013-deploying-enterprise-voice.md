---
title: Lync Server 2013：部署企業語音
TOCTitle: 部署企業語音
ms:assetid: b5b593a6-ac30-461c-8c8c-0041e2c9ab04
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412876(v=OCS.15)
ms:contentKeyID: 49292069
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中部署企業語音

 

_**上次修改主題的時間：** 2012-10-03_

Lync Server 2013、 企業語音 是 Lync Server 2013 基礎結構的部分。

若要部署 Enterprise Voice，您需要進行下列動作：

1.  閱讀規劃文件中的 [在 Lync Server 2013 中規劃企業語音](lync-server-2013-planning-for-enterprise-voice.md)一節。

2.  完成與此工作量一同部署之功能與元件的計劃。

3.  執行 規劃工具來設計拓撲，以反映您的部署決策。

4.  在 拓撲產生器中開啟拓撲設計，如部署文件中的 [在 Lync Server 2013 中定義和設定拓撲](lync-server-2013-defining-and-configuring-the-topology.md) 所述。
    
    > [!NOTE]  
    > 拓撲產生器的安裝屬於內部集區的部署程序。如需詳細資訊，請參閱部署文件中的 <a href="lync-server-2013-install-lync-server-administrative-tools.md">安裝 Lync Server 2013 系統管理工具</a>。
    


此外，您必須已在對應您選擇部署之參考拓撲的中央網站和分支網站部署 Lync Server Enterprise Edition。除非您已至少針對一個內部集區定義、發行且安裝檔案，否則無法部署 企業語音元件，而且您必須使用 拓撲產生器定義和發行內部集區。

若要檢視其中提供能夠部署 企業語音伺服器角色之位置範例的參考拓撲 (及其彼此之間和其他 Lync Server 2013 伺服器角色之間的關聯性)，請參閱規劃文件中的 [Lync Server 2013 中的參考拓撲](lync-server-2013-reference-topologies.md)。

若要檢視顯示及說明範例通話許可控制部署的參考拓撲，包括網路地區、網站及子網路，請參閱 [範例：在 Lync Server 2013 中收集通話許可控制服務需求](lync-server-2013-example-of-gathering-your-requirements-for-call-admission-control.md)。

> [!IMPORTANT]  
> 若要在中央網站部署 企業語音，請繼續閱讀本節中的主題。若要在分支網站部署 企業語音，請跳至部署文件中的 <a href="lync-server-2013-deploying-branch-sites.md">在 Lync Server 2013 中部署分支網站</a>。



本章節包括中繼伺服器配置於每一部前端伺服器或 Standard Edition Server 上 (建議方式) 的部署程序，以及採用獨立中繼伺服器集區的部署程序。

如果您是使用 拓撲產生器定義和發行在每一部前端伺服器或 Standard Edition Server 上配置中繼伺服器的拓撲，可以跳至以下內容，因為 \[部署精靈\] 已在您為前端伺服器集區或 Standard Edition Server 安裝檔案時，自動為中繼伺服器安裝檔案：

  - [在 Lync Server 2013 中設定主幹](lync-server-2013-configuring-trunks.md)

如果您是使用 拓撲產生器 在獨立集區中定義和發佈中繼伺服器，可以使用下列內容：

  - 確認您的拓撲符合軟體和環境先決條件，如 [Lync Server 2013 的企業語音先決條件](lync-server-2013-enterprise-voice-prerequisites.md)\>中所述。

## 本節內容

   [Lync Server 2013 的企業語音先決條件](lync-server-2013-enterprise-voice-prerequisites.md)

   [在 Lync Server 2013 中部署中繼伺服器並定義對等項目](lync-server-2013-deploying-mediation-servers-and-defining-peers.md)

   [在 Lync Server 2013 中設定主幹](lync-server-2013-configuring-trunks.md)

   [在 Lync Server 2013 中設定撥號對應表](lync-server-2013-configuring-dial-plans.md)

   [在 Lync Server 2013 中設定語音原則、PSTN 使用方式記錄和語音路由](lync-server-2013-configuring-voice-policies-pstn-usage-records-and-voice-routes.md)

   [在 Lync Server 2013 中匯出和匯入語音路由組態](lync-server-2013-exporting-and-importing-voice-routing-configuration.md)

   [在 Lync Server 2013 中測試語音路由](lync-server-2013-test-voice-routing.md)

   [在 Lync Server 2013 中發佈擱置變更至語音路由設定](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)

   [部署內部部署的 Exchange UM，以提供 Lync Server 2013 語音信箱](lync-server-2013-deploying-on-premises-exchange-um-to-provide-lync-server-2013-voice-mail.md)

   [在主控 Exchange UM 上提供 Lync Server 2013 使用者語音信箱](lync-server-2013-providing-lync-server-users-voice-mail-on-hosted-exchange-um.md)

   [設定內部部署 Lync Server 2013 與 Exchange Online 整合](lync-server-2013-configuring-on-premises-lync-server-integration-with-exchange-online.md)

   [在 Lync Server 2013 中部署進階 Enterprise Voice 功能](lync-server-2013-deploying-advanced-enterprise-voice-features.md)
    
    - [關於 Lync Server 2013 中的網路區域、網站和子網路](lync-server-2013-about-network-regions-sites-and-subnets.md)
    
    - [在 Lync Server 2013 中建立或修改網路地區](lync-server-2013-create-or-modify-a-network-region.md)
    
    - [在 Lync Server 2013 中建立或修改網站](lync-server-2013-create-or-modify-a-network-site.md)
    
    - [在 Lync Server 2013 中建立子網路與網路站台的關聯](lync-server-2013-associate-a-subnet-with-a-network-site.md)
    
    - [在 Lync Server 2013 中設定通話許可控制](lync-server-2013-configure-call-admission-control.md)
    
    - [在 Lync Server 2013 中設定增強型 9-1-1](lync-server-2013-configure-enhanced-9-1-1.md)
    
    - [在 Lync Server 2013 中設定媒體旁路](lync-server-2013-configure-media-bypass.md)

   [在 Lync Server 2013 中為使用者啟用企業語音](lync-server-2013-enable-users-for-enterprise-voice.md)

## 請參閱

#### 其他資源

[在 Lync Server 2013 中部署分支網站](lync-server-2013-deploying-branch-sites.md)  
[在 Lync Server 2013 中設定撥入會議](lync-server-2013-configuring-dial-in-conferencing.md)  
[在 Lync Server 2013 中設定通話駐留](lync-server-2013-configuring-call-park.md)  
[在 Lync Server 2013 中設定未指派號碼的宣告](lync-server-2013-configuring-announcements-for-unassigned-numbers.md)  
[在 Lync Server 2013 中部署監控](lync-server-2013-deploying-monitoring.md)

