---
title: Lync Server 2013：SIP 主幹連線
TOCTitle: SIP 主幹連線
ms:assetid: 7c586401-d0e5-4017-b3e1-fe5e7f8fc6db
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398619(v=OCS.15)
ms:contentKeyID: 49291450
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 SIP 主幹連線

 

_**上次修改主題的時間：** 2012-08-13_

工作階段初始通訊協定 (SIP) 可用來為基本電話服務與其他即時通訊服務 (如立即訊息、會議、顯示狀態偵測和多媒體等) 啟動及管理 VoIP 通訊工作階段。本節將提供實作「SIP 主幹」 的規劃資訊，這是一種可延伸到您區域網路邊界以外的 SIP 連線。

## 何謂 SIP 主幹？

SIP 主幹是一種 IP 連線，可在您的組織與網際網路電話語音服務提供者 (ITSP) 之間建立延伸到防火牆以外的 SIP 通訊連結。一般而言，SIP 主幹會用來將組織的中央網站連線至 ITSP。有時候，您也可能會選擇使用 SIP 主幹將分支網站連線至 ITSP。

## SIP 主幹與直接 SIP 連線的比較

「主幹」一詞衍生自電路交換技術。它是指連接電話交換設備的專用實體線路。如同其前身 (即分時多工 (TDM) 主幹)，SIP 主幹是兩個不同 SIP 網路 (Lync Server 2013 企業和 ITSP) 之間的連線。與電路交換主幹不同之處在於，SIP 主幹是可以透過任何支援的 SIP 主幹連線類型建立的虛擬連線。如需支援連線類型的詳細資訊，請參閱[如何在 Lync Server 2013 中實作 SIP 主幹？](lync-server-2013-how-do-i-implement-sip-trunking.md)。

另一方面，直接 SIP 連線是未穿越區域網路邊界的 SIP 連線 (亦即，它們是連線至位於您內部網路中的公用交換電話網路 (PSTN) 閘道或專用交換機 (PBX))。如需如何對 Lync Server 2013 使用直接 SIP 連線的詳細資訊，請參閱＜ [Lync Server 2013 中的 SIP 直接連線](lync-server-2013-direct-sip-connections.md)＞。

## 本節內容

  - [Lync Server 2013 中的 SIP 主幹連線概觀](lync-server-2013-overview-of-sip-trunking.md)

  - [如何在 Lync Server 2013 中實作 SIP 主幹？](lync-server-2013-how-do-i-implement-sip-trunking.md)

  - [Lync Server 2013 中的 SIP 主幹連線的元件與拓撲](lync-server-2013-components-and-topologies-for-sip-trunking.md)

  - [Lync Server 2013 中的分支網站 SIP 主幹連線](lync-server-2013-branch-site-sip-trunking.md)

  - [Lync Server 2013 的 SIP 主幹部署檢查表](lync-server-2013-sip-trunk-deployment-checklist.md)

