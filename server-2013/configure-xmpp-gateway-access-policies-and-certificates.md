---
title: 設定 XMPP 閘道存取原則及憑證
TOCTitle: 設定 XMPP 閘道存取原則及憑證
ms:assetid: fac02f4e-d14d-4be3-b53c-74c82436fd93
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721945(v=OCS.15)
ms:contentKeyID: 49890515
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 XMPP 閘道存取原則及憑證

 

_**上次修改主題的時間：** 2012-10-15_

XMPP 同盟會根據「可延伸訊息與目前狀態通訊協定」(XMPP) 定義外部部署。XMPP 設定可讓 Lync 使用者以下列方式存取 XMPP 網域使用者：

  - IM 與目前狀態 – 僅人員對人員

  - 在 Lync 用戶端中建立 XMPP 同盟連絡人

設定原則以支援可延伸訊息與目前狀態通訊協定 (XMPP) 同盟夥伴時，原則會套用至 XMPP 同盟網域，但不會套用至工作階段初始通訊協定 (SIP) 即使訊息 (IM) 服務提供者 (例如 Windows Live) 的使用者或 SIP 同盟網域。您要為每個 XMPP 同盟網域設定想讓使用者新增連絡人並可相互通訊的 XMPP 同盟夥伴。一旦實施原則，就必須設定 XMPP 閘道憑證。

> [!NOTE]  
> 若要開始 XMPP 閘道移轉，您必須部署 Lync Server 2013 XMPP 閘道，並設定存取原則，以啟用 Lync Server 2013 XMPP 閘道的使用者。執行這些步驟前，必須先將所有使用者移至 Lync Server 2013 部署。如需詳細資訊，請參閱 <a href="configure-xmpp-gateway-on-lync-server-2013.md">在 Lync Server 2013 設定 XMPP 閘道</a>。



## 設定外部存取原則以啟用 Lync Server 2013 XMPP 閘道的使用者

1.  開啟 Lync Server 控制台。

2.  在左導覽列中，依序按一下 \[同盟與外部存取\] 和 \[外部存取原則\] 。

3.  依序按一下 \[新增\] 和 \[使用者原則\] 。

4.  輸入外部存取使用者原則的名稱。

5.  提供外部存取使用者原則的描述。

6.  選取 \[啟用與同盟使用者的通訊\] 。

7.  選取 \[啟用與XMPP 同盟使用者的通訊\] 。

8.  按一下 \[認可\] 將變更儲存至網站或使用者原則。

