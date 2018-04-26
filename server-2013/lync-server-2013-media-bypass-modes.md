---
title: Lync Server 2013：媒體旁路模式
TOCTitle: 媒體旁路模式
ms:assetid: 38c06c81-7e45-4423-9e00-7fbfa4befe46
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425862(v=OCS.15)
ms:contentKeyID: 49290612
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的媒體旁路模式

 

_**上次修改主題的時間：** 2012-10-05_

您必須設定全域媒體旁路，並針對每個個別 PSTN 主幹設定媒體旁路。啟用全域媒體旁路時，有兩個選項： **\[永遠略過\]** 和 **\[使用站台和區域資訊\]** 。

如名稱所述， **\[永遠略過\]** 代表會對所有 PSTN 通話嘗試使用旁路。 **\[永遠略過\]** 用於不需要啟用通話許可控制的部署，以及不需要指定何時採用媒體旁路之設定詳細資訊的部署。此外， **\[永遠略過\]** 也用於用戶端和 PSTN 閘道間有完整連線時。在此設定中，所有子網路都會對應至一個 (且恰只一個) 由系統計算的旁路 ID。

若採用 **\[使用站台和區域資訊\]** ，則會使用與網站和區域設定關聯的旁路 ID 來進行旁路決策。此設定可提供替大部分常見技術設定旁路的彈性，因為它可讓您細微控制何時進行旁路，並支援與通話許可控制 (CAC) 的互動。系統會根據以下規則，自動指派旁路 ID，以減輕您的工作。

  - 系統自動指派單一的唯一旁路 ID 給每個區域。

  - 透過 WAN 連結連線至區域且無頻寬限制的網站，會繼承該區域的相同旁路 ID。

  - 透過 WAN 連結與區域產生關聯但有頻寬限制的網站，獲指派的旁路 ID 將與區域不同。

  - 與每個網站關聯的子網路，繼承該網站的旁路 ID。

## 請參閱

#### 概念

[Lync Server 2013 中的媒體旁路概觀](lync-server-2013-overview-of-media-bypass.md)  
[Lync Server 2013 中的媒體旁路和通話許可控制](lync-server-2013-media-bypass-and-call-admission-control.md)  
[Lync Server 2013 中媒體旁路的技術需求](lync-server-2013-technical-requirements-for-media-bypass.md)

