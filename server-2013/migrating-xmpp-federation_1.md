---
title: 移轉 XMPP 同盟
TOCTitle: 移轉 XMPP 同盟
ms:assetid: 7368ee8f-a201-4d3a-b4e8-68396b156d4d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688093(v=OCS.15)
ms:contentKeyID: 49890115
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉 XMPP 同盟

 

_**上次修改主題的時間：** 2012-10-16_

舊版 Office Communications Server 提供的 Extensible Messaging and Presence Protocol (XMPP) 閘道可部署為個別伺服器角色以允許與 XMPP 部署建立同盟。在 Lync Server 2013 中，XMPP 功能可部署為功能。XMPP 功能可以兩個部分進行安裝：執行於 Lync Server 2013 Edge Server 的 XMPP Proxy，以及執行於 Lync Server 2013 前端伺服器的 XMPP 閘道。

就移轉方面而言，可將 Office Communications Server 2007 R2 使用者帳戶移至 Lync Server 2013 集區，然後再繼續使用 Office Communications Server 2007 R2 XMPP 閘道。這只有在 Lync Server 2013 未設定 XMPP 同盟合作夥伴時才能實現。

總結來說，如果 Office Communications Server 已部署 Office Communications Server 2007 R2 XMPP 閘道，且已為舊版 Office Communications Server 2007 R2 使用者啟用 XMPP 同盟，若要將 XMPP 同盟移轉至 Lync Server 2013，請進行下列動作：

1.  部署 Lync Server 2013 集區。

2.  部署 Lync Server 2013 Edge Server。

3.  將所有使用者移至 Lync Server 2013 集區。

4.  建立 Edge Server 的 XMPP 存取原則與憑證。

5.  在 Lync Server 2013 中啟用 XMPP 同盟。 

6.  將 DNS 項目更新為指向 Lync Server 2013 XMPP 閘道。

