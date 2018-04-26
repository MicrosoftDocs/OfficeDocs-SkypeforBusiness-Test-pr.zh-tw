---
title: Lync Server 2013：使用 SIP 主幹路由 E9-1-1 來電
TOCTitle: 使用 SIP 主幹路由 E9-1-1 來電
ms:assetid: 157753c3-fe74-4e2c-81da-ee06911d4cc2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204701(v=OCS.15)
ms:contentKeyID: 49290191
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中使用 SIP 主幹路由 E9-1-1 來電

 

_**上次修改主題的時間：** 2012-09-29_

使用 SIP 主幹來連線到合格的 E9-1-1 服務提供者，是部署 E9-1-1 的方式之一。如需使用 ELIN 閘道來連線到公用交換電話網路 (PSTN) 型 E9-1-1 服務提供者的詳細資訊，請參閱＜ [在 Lync Server 2013 中使用 ELIN 閘道路由 E9-1-1 來電](lync-server-2013-routing-e9-1-1-calls-by-using-an-elin-gateway.md)＞。

下圖顯示當您使用 SIP 主幹及合格的 E9-1-1 服務提供者時，緊急通話如何從 Lync Server 路由傳送至公共安全勤務中心 (PSAP)。

**透過 SIP 主幹路由傳送 E9-1-1 通話**

![將緊急電話從 Lync Server 路由傳送至 PSAP](images/JJ204701.0637a9d4-2ca7-438a-8ed0-19090a4b992d(OCS.15).jpg "將緊急電話從 Lync Server 路由傳送至 PSAP")

緊急電話是從相容的 Lync Server 用戶端撥出時：

1.  包含位置、發話者回撥號碼，以及 (選用) 通知 URL 和會議回撥號碼的 SIP INVITE，會路由傳送到 Lync Server。

2.  Lync Server 會比對緊急電話號碼，並將通話路由傳送 (依據適用位置原則中定義的 \[PSTN 使用方式\] 值) 至 中繼伺服器，並且從那裡透過 SIP 主幹路由傳送至 E9-1-1 服務提供者。

3.  E9-1-1 服務提供者會依據隨附於通話的位置，將緊急通話路由傳送至正確的 PSAP。當用戶端將驗證過的緊急回應位置 (ERL) 隨附於緊急通話，提供者會自動將通話路由傳送至適當的 PSAP。如果位置是由使用者手動輸入，緊急通話回應中心 (ECRC) 會先向發話者口頭確認位置的精確度，才將緊急通話路由傳送至 PSAP。

4.  如果您已設定通知的位置原則，就會將特殊的 Lync 緊急通知立即訊息傳送給組織的一或多個安全人員。此訊息一律會快顯在安全人員的螢幕上，並包含發話者的名稱、電話號碼、時間和位置，讓安全人員能夠使用立即訊息或語音，快速回應緊急發話者。

5.  如果您設定了會議的位置原則，且其受到 E9-1-1 服務提供者支援，則內部安全性桌面會以單向音訊或雙向音訊加入電話會議。

6.  如果通話突然中斷，PSAP 會直接使用回撥號碼來連絡發話者。

