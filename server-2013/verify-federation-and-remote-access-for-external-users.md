---
title: 確認外部使用者的同盟及遠端存取
TOCTitle: 確認外部使用者的同盟及遠端存取
ms:assetid: a383fefb-c428-4462-93fd-15ba540fa867
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688163(v=OCS.15)
ms:contentKeyID: 49890243
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 確認外部使用者的同盟及遠端存取

 

_**上次修改主題的時間：** 2012-09-18_

將同盟路由轉換至 Lync Server 2013  Edge Server 時，應該執行一些功能測試，以確認同盟如預期般執行。外部使用者存取的測試應該包含組織支援的每種外部使用者類型，包括下列任一項或所有項目。

## 測試外部使用者與外部存取連線能力

  - 來自至少一個同盟網域的使用者，一位內部使用者在 Lync Server 2013 上，另一位使用者在 Lync Server 2010 上。測試立即訊息 (IM)、目前狀態、音訊/視訊 (A/V) 及桌面共用。

  - 讓各個組織支援 (且已佈建完成) 的公用 IM 服務提供者的使用者與 Lync Server 2013 上的使用者及 Lync Server 2010 上的使用者進行通訊。

  - 確認匿名使用者可以加入會議。

  - 位於 Lync Server 2010 上並使用遠端使用者存取的使用者 (非使用 VPN 而從內部網路外部登入 Lync Server 2010) 與位於 Lync Server 2013 上的使用者，以及位於 Lync Server 2010 上的使用者。測試 IM、目前狀態、A/V 及桌面共用。

  - 位於 Lync Server 2013 上並使用遠端使用者存取的使用者 (非使用 VPN 而從內部網路外部登入 Lync Server 2013) 與位於 Lync Server 2013 上的使用者，以及位於 Lync Server 2010 上的使用者。測試 IM、目前狀態、A/V 及桌面共用。

