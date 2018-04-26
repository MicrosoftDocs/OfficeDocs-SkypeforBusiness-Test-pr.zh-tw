---
title: Lync Server 2013：新主幹功能
TOCTitle: 新主幹功能
ms:assetid: 9b398bc8-2760-4218-b1a4-89b9694b1171
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688152(v=OCS.15)
ms:contentKeyID: 49890228
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的新主幹功能

 

_**上次修改主題的時間：** 2012-09-21_

在 Microsoft Lync Server 2013 中， 中繼伺服器和閘道之間可以定義多個主幹。 Microsoft Lync Server 2010 只允許 中繼伺服器和 PSTN 閘道之間有單一主幹。此功能可提供定義額外主幹所需的彈性。主幹是 中繼伺服器 FQDN 加聆聽連接埠和 PSTN 閘道 FQDN 加聆聽連接埠之間的邏輯關聯。這項新功能可以輕易定義擁有恢復能力所需的主幹 (使用多部中繼伺服器將通話路由傳送至同一個 PSTN 閘道)、PBX 互通性 (在 IP-PBX 和 中繼伺服器之間使用多個具有不同相關聯原則的主幹)，以及特定的 SIP 主幹組態 (使不同網站的 中繼伺服器都有主幹可連到以相同業者 FQDN 指出的業者)。

## 請參閱

#### 概念

[Lync Server 2013 中的新企業語音功能](lync-server-2013-new-enterprise-voice-features.md)

