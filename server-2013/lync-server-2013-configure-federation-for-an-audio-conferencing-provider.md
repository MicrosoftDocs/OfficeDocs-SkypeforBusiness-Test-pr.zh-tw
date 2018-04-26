---
title: Lync Server 2013：針對音訊會議提供者設定同盟
TOCTitle: 針對音訊會議提供者設定同盟
ms:assetid: 08dedcce-0d3f-45da-8282-cf2634a41665
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn510996(v=OCS.15)
ms:contentKeyID: 59955438
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中針對音訊會議提供者設定同盟

 

_**上次修改主題的時間：** 2014-07-24_

若要在混合式部署 (包含 Lync Online 的 Lync Server 內部部署) 中使用音訊會議提供者 (ACP)，您需要在內部部署的 Lync 部署及作為允許的協力廠商伺服器的 ACP 協力廠商之間設定同盟。若要設定同盟，請將 ACP 協力廠商網域與 Edge Server (這也可能稱為「存取 Proxy」) 新增至內部部署的 \[同盟網域\] 清單。接著，您的 ACP 協力廠商需要將您內部部署 Edge Server 集區的 FQDN 新增至其允許的同盟網域清單。如需其他詳細資訊，請連絡您的 ACP 提供者。接著，您的 ACP 協力廠商需要將您內部部署 Edge Server 集區的 FQDN 新增至其允許的同盟網域清單。

  - **新增 ACP 網域和 Edge Server 為允許的同盟網域**
    
    若要將 ACP 網域新增為允許的協力廠商伺服器 (允許的同盟網域)，請遵循 [在 Lync Server 2013 中針對允許的外部網域設定支援](lync-server-2013-configure-support-for-allowed-external-domains.md)中的步驟操作。對於 Edge Server，請新增 ACP 協力廠商的 Edge Server FQDN。您可能需要連絡您的 ACP 協力廠商，以取得其 Edge Server 的 FQDN (也就是您的 ACP 所稱的「存取 Proxy」)。

  - **提供您 Edge Server 集區的 FQDN 給 ACP 協力廠商**
    
    ACP 協力廠商需要設定同盟，將您 Edge Server 集區的 FQDN 新增為允許的同盟網域，才可將您的內部部署網域新增為允許的協力廠商伺服器。

