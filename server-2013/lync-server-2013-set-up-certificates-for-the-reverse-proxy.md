---
title: Lync Server 2013：設定反向 Proxy 的憑證
TOCTitle: 設定反向 Proxy 的憑證
ms:assetid: c03a08ec-a67b-4f11-b0d7-6677461beaaa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412938(v=OCS.15)
ms:contentKeyID: 49292201
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定反向 Proxy 的憑證

 

_**上次修改主題的時間：** 2012-09-08_

每一部反向 Proxy 伺服器都需要有網頁伺服器憑證可供接聽服務使用。網頁伺服器憑證必須由公用憑證授權單位 (CA) 發行。

如需有關此憑證與其他憑證需求的詳細資訊，請參閱＜ [Lync Server 2013 中的外部使用者存取的憑證需求](lync-server-2013-certificate-requirements-for-external-user-access.md)＞。

## 若要設定反向 Proxy 的 Web 服務憑證

  - 您應已完成反向 Proxy 的設定，包括設定 Web 服務憑證。如果在開始部署 Edge Server 前尚未執行此操作，請利用[設定 Lync Server 2013 的反向 Proxy 伺服器](lync-server-2013-setting-up-reverse-proxy-servers.md)中的程序建立要求並安裝 Web 服務憑證，然後建立各個 Web 發行規則並設為使用此憑證。

