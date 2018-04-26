---
title: Lync Server 2013：SIP 直接連線
TOCTitle: SIP 直接連線
ms:assetid: 0a37737d-9628-4e36-b27b-c134fa5a3882
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398151(v=OCS.15)
ms:contentKeyID: 49290034
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 SIP 直接連線

 

_**上次修改主題的時間：** 2012-08-13_

您可以使用「直接 SIP 連線」 將 Lync Server 連線至下列任一項目：

  - IP-PBX (如需詳細資訊，請參閱＜ [Lync Server 2013 中的 SIP 直接部署選項](lync-server-2013-direct-sip-deployment-options.md)＞)。

  - PSTN 閘道 (如需詳細資訊，請參閱＜ [Lync Server 2013 中的 PSTN 閘道部署選項](lync-server-2013-pstn-gateway-deployment-options.md)＞)。

若要實作直接 SIP 連線，基本上遵循您用於實作 SIP 主幹的相同部署步驟。在這兩種情況下，您都會使用 中繼伺服器的外部介面實作連線。唯一的差異在於您將 SIP 主幹連線至外部實體 (如 ITSP 閘道)，而將直接 SIP 連線連接至區域網路中的內部實體 (如 IP-PBX 或公用交換電話網路 (PSTN) 閘道)。

## 本節內容

  - [Lync Server 2013 中的 SIP 直接部署選項](lync-server-2013-direct-sip-deployment-options.md)

  - [Lync Server 2013 中的 PSTN 閘道部署選項](lync-server-2013-pstn-gateway-deployment-options.md)

