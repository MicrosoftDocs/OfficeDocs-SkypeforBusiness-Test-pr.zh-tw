---
title: Lync Server 2013：通話許可控制和中繼伺服器
TOCTitle: 通話許可控制和中繼伺服器
ms:assetid: 76faccdc-67d0-4c8b-8e47-1e23c93b02c6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398585(v=OCS.15)
ms:contentKeyID: 49291366
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的通話許可控制和中繼伺服器

 

_**上次修改主題的時間：** 2012-09-21_

通話許可控制服務 (CAC) 是首次引進 Lync Server 2010，可根據可用頻寬來管理即時建立的工作階段，避免讓壅塞網路上的使用者感到經驗品質 (QoE) 不良。為了支援此功能，中繼伺服器 (在 企業語音基礎結構與閘道或 SIP 主幹提供者之間提供訊號與媒體轉譯機制) 負責管理此功能在 Lync Server 端與閘道端上的兩種互動所使用的頻寬。在通話許可控制服務中，通話的終端實體負責處理頻寬保留。 中繼伺服器在閘道端上互動的閘道對等 (PSTN 閘道、IP-PBX、SBC) 並不支援 Lync Server 2013 通話許可控制服務。因此， 中繼伺服器必須代表其閘道對等處理頻寬互動。只要情況允許， 中繼伺服器即會事先保留頻寬。如果情況不允許 (例如，撥出至閘道對等時，如果閘道端上最終媒體端點的位置不明)，則會在撥打電話時保留頻寬。此行為可能會導致頻寬超額的情況，但這是防止撥號錯誤的唯一方式。

媒體旁路與頻寬保留是互斥的。如果對某通電話使用了媒體旁路，即無法再對其執行通話許可控制服務。此處是假設與電話有關的連結都沒有頻寬受限的情形。如果對某通電話使用涉及 中繼伺服器的通話許可控制服務，該通電話即無法使用媒體旁路。

如需媒體旁路或通話許可控制的詳細資訊，請參閱規劃文件中的＜ [在 Lync Server 2013 中規劃媒體旁路](lync-server-2013-planning-for-media-bypass.md)＞或＜ [在 Lync Server 2013 中規劃通話許可控制](lync-server-2013-planning-for-call-admission-control.md)＞。

