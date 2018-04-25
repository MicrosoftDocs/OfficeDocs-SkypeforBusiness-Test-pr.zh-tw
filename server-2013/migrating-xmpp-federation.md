---
title: 移轉 XMPP 同盟
TOCTitle: 移轉 XMPP 同盟
ms:assetid: b8d2b4b9-d0ed-4b48-820a-2c257fbdd2fb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721861(v=OCS.15)
ms:contentKeyID: 49890278
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉 XMPP 同盟

 

_**上次修改主題的時間：** 2012-10-19_

舊版的 Lync Server 和 Office Communications Server 提供可延伸傳訊和顯示狀態通訊協定 (XMPP) 閘道，此閘道可部署為個別的伺服器角色，以允許與 XMPP 部署進行同盟。在 Lync Server 2013 中，可將 XMPP 部署為功能。XMPP 功能會安裝為兩個部分：在 Lync Server 2013 Edge Server 伺服器上執行的 XMPP Proxy 與在 Lync Server 2013 前端伺服器上執行的 XMPP 閘道。

從移轉的概念來看，可將 Lync Server 使用者帳戶移至 Lync Server 2013 集區，並繼續使用舊版 XMPP 閘道。當 Lync Server 2013 中未設定 XMPP 同盟協力廠商時，才能這樣做。

總結來說，如果 Lync Server 2010 已部署 Office Communications Server 2007 R2 XMPP 閘道，且已為舊版 Lync Server 2010 使用者啟用 XMPP 同盟，若要將 XMPP 同盟移轉至 Lync Server 2013，請進行下列動作：

1.  部署 Lync Server 2013 集區。

2.  部署 Lync Server 2013 Edge Server。

3.  將所有使用者移至 Lync Server 2013 集區。

4.  建立 Edge Server 的 XMPP 存取原則與憑證。

5.  在 Lync Server 2013 中啟用 XMPP 同盟。 

6.  將 DNS 項目更新為指向 Lync Server 2013 XMPP 閘道。

