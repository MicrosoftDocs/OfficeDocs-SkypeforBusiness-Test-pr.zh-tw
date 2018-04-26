---
title: Lync Server 2013：多主幹支援
TOCTitle: 多主幹支援
ms:assetid: a1309c09-ad9a-4c54-9650-4e3f5b2a4a00
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205127(v=OCS.15)
ms:contentKeyID: 49291867
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的多主幹支援

 

_**上次修改主題的時間：** 2012-11-01_

Lync Server 2013 功能支援閘道與 中繼伺服器之間的多重關聯。定義主幹即可建立這些關聯，而主幹是 中繼伺服器集區與公用交換電話網路 (PSTN) 閘道、工作階段邊界控制器 (SBC) 或 IP-PBX 之間的邏輯關聯。使用 拓撲產生器讓閘道與中繼伺服器 (也就是主幹) 產生關聯。

  - 若要在 Lync Server 2013 中指派或移除主幹，您必須先在 拓撲產生器中定義主幹。主幹是由以下關聯所組成： 中繼伺服器完整網域名稱 (FQDN)、 中繼伺服器聆聽連接埠、閘道 FQDN 和閘道聆聽連接埠。

  - 若要設定多個主幹，您可以在相同閘道與 中繼伺服器之間建立多重關聯。這樣可對 企業語音基礎架構提供額外的恢復功能，尤其適合用於專用交換機 (PBX) 交互操作案例中。

主幹在定義後就必須與路由建立關聯。若要建立主幹與路由的關聯，您可在 拓撲產生器中定義主幹的簡單名稱。在主幹與路由可建立關聯的 Lync Server 控制台中，此簡單名稱會做為主幹名稱。簡單主幹名稱會做為 Lync Server 管理命令介面中的閘道名稱。

    New-CsVoiceRoute -Identity <RouteId> -NumberPattern <String> -PstnUsages @{add="<UsageString>"} -PstnGatewayList @{add="<TrunkSimpleName>"}

系統管理員必須選取與 中繼伺服器相關聯的預設主幹。在 拓撲產生器中用滑鼠右鍵按一下相關聯的 中繼伺服器，然後按一下 \[內容\] 。指定 中繼伺服器的預設閘道。

下圖說明針對每個 中繼伺服器和閘道定義的多個主幹。

**M-N 主幹路由**

![多重主幹指派。](images/JJ205127.c61cd9a7-d8d9-4e02-83b9-ab62519a48c4(OCS.15).jpg "多重主幹指派。")

