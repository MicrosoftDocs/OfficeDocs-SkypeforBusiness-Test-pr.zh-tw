---
title: Lync Server 2013 主控 Exchange UM 整合支援
TOCTitle: 主控 Exchange UM 整合支援
ms:assetid: c7573ec3-013c-48d9-b59b-2a5427e6da35
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398821(v=OCS.15)
ms:contentKeyID: 49292287
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的主控 Exchange UM 整合支援

 

_**上次修改主題的時間：** 2012-09-21_

Lync Server 2013 ExUM 路由應用程式支援與內部部署環境中的 Exchange 整合通訊 (UM) 整合 (其中 Lync Server 2013 和 Exchange UM 都是在您企業內部本機安裝)，或是支援與服務提供者所裝載的 Exchange UM 整合，如下圖所示。

![內部部署 Lync Server Exchange UM 部署](images/Gg398821.d6498eb9-87ee-40f3-8ecd-852f91546590(OCS.15).jpg "內部部署 Lync Server Exchange UM 部署")

支援下列模式：

  - **內部部署模式**    Lync Server 2013 和 Exchange UM 都會在您企業內部的本機伺服器上部署。

  - **跨部署模式**    Lync Server 2013 會在您企業內部的本機伺服器上部署，而 Exchange UM 則會在線上服務提供者的設備中裝載，例如 Microsoft Exchange 線上資料中心。

  - **混合模式**   在您的 Lync Server 2013 部署中，有一些使用者信箱隸屬於您企業中執行 Microsoft Exchange Server 的本機伺服器，還有一些信箱隸屬於託管式 Exchange 服務資料中心。
    
    > [!NOTE]  
    > 在評估及逐步移轉使用者至託管式 Exchange UM 期間，混合模式可當作過渡時期解決方案使用；或者，如果您選擇在移轉部分使用者後，使剩餘使用者的 Exchange UM 服務保持內部部署，則該模式可當作永久解決方案使用。
    


若要將 Lync Server 2013 與託管式 Exchange UM 整合，必須設定「共用 SIP 位址空間」 (也稱為「分割網域」 )。在此設定中， Lync Server 2013 和第三方託管式 Exchange UM 服務提供者都能存取相同的 SIP 網域位址空間。如需詳細資訊，請參閱規劃文件中的 [Lync Server 2013 中的主控 Exchange UM 整合架構](lync-server-2013-hosted-exchange-um-integration-architecture.md)。

