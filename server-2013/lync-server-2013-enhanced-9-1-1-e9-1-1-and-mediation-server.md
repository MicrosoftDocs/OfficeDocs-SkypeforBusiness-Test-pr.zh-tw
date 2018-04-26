---
title: Lync Server 2013：增強型 9-1-1 (E9-1-1) 和中繼伺服器
TOCTitle: 增強型 9-1-1 (E9-1-1) 和中繼伺服器
ms:assetid: d231221f-5596-4a87-a463-269f5bcce65f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398903(v=OCS.15)
ms:contentKeyID: 49292410
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的增強型 9-1-1 (E9-1-1) 和中繼伺服器

 

_**上次修改主題的時間：** 2012-09-29_

中繼伺服器具備延伸的功能，以便能夠正確地與增強型 9-1-1 (E9-1-1) 服務提供者互動。不需要在中繼伺服器上進行任何特殊設定，E9-1-1 互動所需的 SIP 延伸預設會包含在中繼伺服器的 SIP 通訊協定中，以支援它與閘道對等 (PSTN 閘道、IP-PBX，或網際網路電話語音服務提供者的 SBC，包括 E9-1-1 服務提供者) 的互動。

連到 E9-1-1 服務提供者的 SIP 主幹是否能在現有中繼伺服器集區上終止，或者需要獨立的中繼伺服器，取決於 E9-1-1 SBC 是否能與中繼伺服器的集區互動。如需詳細資訊，請參閱＜ [Lync Server 2013 中的 M:N 主幹](lync-server-2013-m-n-trunk.md)＞。

