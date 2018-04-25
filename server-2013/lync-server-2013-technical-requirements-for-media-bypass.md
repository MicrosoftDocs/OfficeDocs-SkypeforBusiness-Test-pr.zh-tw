---
title: Lync Server 2013：媒體旁路的技術需求
TOCTitle: 媒體旁路的技術需求
ms:assetid: 6162a204-0e7c-460a-8eb2-e592c6590a8a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398435(v=OCS.15)
ms:contentKeyID: 49291088
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中媒體旁路的技術需求

 

_**上次修改主題的時間：** 2012-09-21_

針對 PSTN 的每個通話， 中繼伺服器會決定是否可以將來自 Lync 來源端點的媒體直接傳送給 中繼伺服器對等，而不需要周遊 中繼伺服器。對等可以是 PSTN 閘道、IP-PBX 或網際網路電話服務提供者 (ITSP) 上的工作階段邊界控制器 (SBC) 與路由通話之中繼伺服器之間的主幹關聯。

符合下列需求時，可以使用媒體旁路：

  - 中繼伺服器對等必須支援媒體旁路的必要功能，其中最重要的是處理多個分支回應 (稱為「早期對話」) 的能力。請連絡閘道或 PBX 製造商或是 ITSP，以取得閘道、PBX 或 SBC 可以接受的早期對話數上限值。

  - 中繼伺服器對等必須接受直接來自 Lync 端點的媒體流量。許多 ITSP 只讓它們的 SBC 接收來自 中繼伺服器的流量。請連絡 ITSP 以確認其 SBC 是否接受直接來自 Lync 端點的媒體流量。

  - Lync 用戶端及 中繼伺服器對等的連線必須良好，這表示它們位在相同的網路地區，或是在透過沒有頻寬限制的 WAN 連結連線至地區的網站

## 請參閱

#### 概念

[Lync Server 2013 中的媒體旁路模式](lync-server-2013-media-bypass-modes.md)  
[Lync Server 2013 中的媒體旁路和通話許可控制](lync-server-2013-media-bypass-and-call-admission-control.md)

