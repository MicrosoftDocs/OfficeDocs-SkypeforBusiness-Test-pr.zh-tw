---
title: 與 Lync Server 2010 都會區網站復原的 Lync Server 2013 相容性
TOCTitle: Lync Server 2010 都會區網站復原
ms:assetid: 18673ff6-b664-4a57-a89b-cbda8b129e6a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204715(v=OCS.15)
ms:contentKeyID: 49290224
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2010 都會區網站復原

 

_**上次修改主題的時間：** 2014-03-19_

支援 Lync Server 2010 的都會網站恢復能力解決方案不支援 Lync Server 2013。這個解決方案會將單一前端集區橫跨同一都會區中的兩個資料中心。

都會網站恢復能力解決方案的設計旨在從遺失整個資料中心的狀況復原。 當您的集區橫跨兩個資料中心時，通常會將一半的前端放進一個資料中心，而另一半放進第二個資料中心。如果您遺失整個資料中心，即遺失了一半的前端伺服器。這會對您在 Lync Server 2013 之前端集區的新分散式系統模型造成問題。如需更多資訊，請參閱 [Lync Server 2013 中的前端伺服器、立即訊息及顯示狀態的拓撲和元件](lync-server-2013-topologies-and-components-for-front-end-servers-instant-messaging-and-presence.md)。

