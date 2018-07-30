---
title: Lync Server 2013：內部部署 Unified Messaging 的元件和拓撲
TOCTitle: 內部部署 Unified Messaging 的元件和拓撲
ms:assetid: 22fc87cf-a7e5-4c8c-bb9b-101e5380cdcf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425711(v=OCS.15)
ms:contentKeyID: 49290342
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中內部部署 Unified Messaging 的元件和拓撲

 

_**上次修改主題的時間：** 2012-09-25_

本主題說明欲提供 Exchange 整合通訊 (UM) 功能給 Lync Server 2013 部署所需的 Microsoft Exchange Server 2013 元件，同時也說明內部部署 Exchange UM 整合的支援拓撲。

## Exchange Server 元件

若要將＜ [整合式 Unified Messaging 和 Lync Server 2013 的功能](lync-server-2013-features-of-integrated-unified-messaging.md)＞中所述的 Exchange UM 功能和服務提供給組織中的 企業語音使用者，您必須部署 Microsoft Exchange 信箱伺服器和 Client Access Server。Client Access Server 可主控使用者信箱並提供電子郵件和語音留言的單一儲存位置。在 Exchange 信箱和 Client Access Server 上， Exchange UM 會以服務的形式來執行。

如需 Microsoft Exchange Server 2007 和 Microsoft Exchange Server 2010 中 Exchange UM 元件的詳細資訊，請參閱部署文件中的＜ [部署內部部署的 Exchange UM，以提供 Lync Server 2013 語音信箱](lync-server-2013-deploying-on-premises-exchange-um-to-provide-lync-server-2013-voice-mail.md)＞。

## 支援的拓撲

您可以將 Lync Server 2013 和 Exchange 整合通訊 (UM) 部署在同一樹系或多個樹系中。如果部署跨越多個樹系，您需對每一個 Exchange UM 樹系執行 Exchange 整合步驟。此外，您也需將每個 Microsoft Exchange 樹系設定為信任 Lync Server 2013 樹系，以及將 Lync Server 2013 樹系設定為信任每個 Exchange UM 樹系。除了此樹系信任外，也需在 Lync Server 2013 樹系的使用者物件中設定所有使用者的 Exchange UM 設定。

Lync Server 2013 支援下列拓撲用於 Exchange UM 整合：

  - 單一樹系

  - 單一網域 (亦即單一樹系搭配單一網域)。 Lync Server 2013、 Microsoft Exchange 和使用者都位於相同網域中。

  - 多重網域 (亦即，一個根網域搭配一或多個子網域)。 Lync Server 2013 和 Microsoft Exchange 伺服器部署的網域不同於用來建立使用者的網域。 Exchange UM 伺服器可以部署在與其支援之 Lync Server 2013 集區不同的網域中。

  - 多重樹系 (亦即資源樹系)。 Lync Server 2013 部署在單一樹系中，接著橫跨多個樹系分散使用者。使用者的 Exchange UM 屬性必須複寫至 Lync Server 2013 樹系。
    
    > [!NOTE]  
    > Exchange 可以部署在多個樹系中。每個 Exchange 組織都能提供 Exchange UM 給其使用者，或是 Exchange UM 可以部署至與 Lync Server 2013 相同的樹系。
    

