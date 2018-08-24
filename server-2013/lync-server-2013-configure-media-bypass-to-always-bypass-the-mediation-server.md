---
title: 在 Lync Server 2013 中設定媒體旁路以一律略過中繼伺服器
TOCTitle: 在 Lync Server 2013 中設定媒體旁路以一律略過中繼伺服器
ms:assetid: 370c4f54-e520-4d77-96a3-84c5e84a9996
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425846(v=OCS.15)
ms:contentKeyID: 49290578
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定媒體旁路以一律略過中繼伺服器

 

_**上次修改主題的時間：** 2013-02-25_

> [!NOTE]
> 本主題假設您已針對想要讓媒體略過中繼伺服器的特定網站或服務，為所有與對等 (公用交換電話網路 (PSTN) 閘道、IP-PBX 或是與網際網路電話語音服務提供者 (ITSP) 的工作階段界限控制器 (SBC)) 的主幹連線設定媒體旁路。<br />
> 您無法設定媒體一律略過中繼伺服器，同時又啟用通話許可控制。這些設定並不相容，因此在 Lync Server 控制台使用者介面中為互斥的設定。


除了針對與中繼伺服器的對等相關聯的個別主幹連線啟用媒體旁路，您還必須設定全域的媒體旁路設定。如果您使用本主題中的步驟來設定全域的媒體旁路設定，則 Lync 端點與任何您已為其主幹連線設定媒體旁路的對等之間必須有良好連線。

如果 Lync Server 端點與中繼伺服器所有對等 (其個別主幹連線已啟用媒體旁路) 之間沒有良好連線，您必須進行全域媒體旁路設定，以在採用媒體旁路時使用網站與地區資訊。如此可對媒體略過中繼伺服器的時機有更精確的控制。若要這樣做，請改為使用[在 Lync Server 2013 中設定媒體旁路全域設定以使用網站和區域資訊](lync-server-2013-configure-media-bypass-global-settings-to-use-site-and-region-information.md)和[在 Lync Server 2013 中建立子網路與網路站台的關聯](lync-server-2013-associate-a-subnet-with-a-network-site.md)中的步驟。

## 全面啟用媒體旁路以永遠略過中繼伺服器

1.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

2.  在左導覽列中，按一下 **\[網路組態\]**。

3.  按兩下清單中的 **\[全域\]** 設定。

4.  在 **\[編輯通用設定\]** 頁面上，選取 **\[啟用媒體旁路\]** 核取方塊。

5.  按一下 **\[永遠略過\]**。

6.  按一下 **\[認可\]**。

## 請參閱

#### 概念

[在 Lync Server 2013 中設定媒體旁路](lync-server-2013-configure-media-bypass.md)  
[Lync Server 2013 中的全域媒體旁路選項](lync-server-2013-global-media-bypass-options.md)  
[Lync Server 2013 中的媒體旁路和中繼伺服器](lync-server-2013-media-bypass-and-mediation-server.md)  

#### 其他資源

[在 Lync Server 2013 中規劃媒體旁路](lync-server-2013-planning-for-media-bypass.md)

