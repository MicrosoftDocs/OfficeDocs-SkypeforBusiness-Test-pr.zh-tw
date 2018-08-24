---
title: Lync Server 2013：關於網路區域、網站和子網路
TOCTitle: 關於網路區域、網站和子網路
ms:assetid: 6662123a-d011-408c-a290-92b2a8589943
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398467(v=OCS.15)
ms:contentKeyID: 49291154
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 關於 Lync Server 2013 中的網路區域、網站和子網路

 

_**上次修改主題的時間：** 2013-02-24_

本節所說明的進階 Enterprise Voice 功能共用網路地區、網站及子網路的特定設定需求。例如，這三個進階功能都需要拓撲中的每個子網路與特定 *「網站」* 相關聯，而且每個網站都必須與 *「網路地區」* 相關聯。

> [!IMPORTANT]  
> 開始通話許可控制、E9-1-1 或媒體旁路的網路設定之前，請確定已檢閱過規劃文件之＜<a href="lync-server-2013-network-settings-for-the-advanced-enterprise-voice-features.md">Lync Server 2013 中的進階企業語音功能的網路設定</a>＞主題中的網路設定相關資訊。如需通話許可控制主要網路設定的詳細資訊，也請參閱規劃文件中的＜<a href="lync-server-2013-defining-your-requirements-for-call-admission-control.md">在 Lync Server 2013 中定義通話許可控制需求</a>＞。



通話許可控制及 E9-1-1 具有其他的網站設定需求：

  - 通話許可控制需要指定透過 WAN 頻寬限制所限制之每個網站的 *「頻寬原則設定檔」* 。如果您計劃部署通話許可控制，則必須先 [在 Lync Server 2013 中建立頻寬原則設定檔](lync-server-2013-create-bandwidth-policy-profiles.md)，再設定網站。

  - E9-1-1 需要指定每個網站的 *「位置原則」* 。如果您計劃部署 E9-1-1，則必須先 [在 Lync Server 2013 中建立位置原則](lync-server-2013-create-location-policies.md)，再設定網站網站。

## 建立或修改網路地區、網站及子網路

下列主題提供網路地區及網站的建立或修改步驟，以及將子網路與網站相關聯的步驟。這些不是任何特定進階 Enterprise Voice 功能特有的主題。

  - [在 Lync Server 2013 中建立或修改網路地區](lync-server-2013-create-or-modify-a-network-region.md)

  - [在 Lync Server 2013 中建立或修改網站](lync-server-2013-create-or-modify-a-network-site.md)

  - [在 Lync Server 2013 中建立子網路與網路站台的關聯](lync-server-2013-associate-a-subnet-with-a-network-site.md)

