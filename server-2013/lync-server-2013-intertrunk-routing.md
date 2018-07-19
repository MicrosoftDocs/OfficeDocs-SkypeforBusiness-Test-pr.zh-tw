---
title: Lync Server 2013：主幹間路由
TOCTitle: 主幹間路由
ms:assetid: d3a33b4a-8bf4-4a8c-a371-8ef79e740780
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205272(v=OCS.15)
ms:contentKeyID: 49292411
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的主幹間路由

 

_**上次修改主題的時間：** 2012-10-20_

Lync Server 2013 可以將 IP-PBX 與公用交換電話網路 (PSTN) 閘道互連，以便將使用 PBX 電話撥打的電話路由至 PSTN，以及將 PSTN 來電路由至專用交換機 (PBX) 電話。同樣地， Lync Server 2013 可以讓兩個以上的 IP-PBX 系統互連，以便可從不同的 IP-PBX 系統在 PBX 電話間撥打和接收電話。

此主幹相互 (intertrunk) 路由功能可使用 Lync Server 管理命令介面 Cmdlet **set-cstrunkconfiguration** 搭配新參數 PstnUsages 來設定。此參數可指定要使用的 PSTN 使用方式記錄。主幹會使用此 PSTN 使用方式來決定路由方式，並據以路由所有來電。

    set-cstrunkconfiguration -Identity <TrunkId> -PstnUsages @{add="<UsageString>"}

下圖說明 Lync Server 2013 在 PSTN 閘道與 IP-PBX 之間提供互連功能。

**閘道與 IP PBX 之間的主幹相互路由功能**

![連接 PSTN 閘道/IP-PBX 圖表的 Lync Server](images/JJ721940.cc3858ca-2ee3-4d51-8a51-db078366b50b(OCS.15).jpg "連接 PSTN 閘道/IP-PBX 圖表的 Lync Server")

下圖說明 Lync Server 2013 交互連接兩個 IP-PBX 系統。

**兩個 IP PBX 之間的主幹相互路由功能**

![交互連接 IP-PAX 系統圖表的 Lync Server](images/JJ721940.6ba18ec9-df70-498a-9cf7-7fc41e5ec432(OCS.15).jpg "交互連接 IP-PAX 系統圖表的 Lync Server")

