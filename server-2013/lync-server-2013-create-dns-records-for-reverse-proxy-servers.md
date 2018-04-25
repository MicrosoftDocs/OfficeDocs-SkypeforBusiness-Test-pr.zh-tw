---
title: Lync Server 2013：建立反向 Proxy 伺服器的 DNS 記錄
TOCTitle: 建立反向 Proxy 伺服器的 DNS 記錄
ms:assetid: b3513339-e49b-4665-80f1-b5a1c81a0e2e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429719(v=OCS.15)
ms:contentKeyID: 49292053
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立反向 Proxy 伺服器的 DNS 記錄

 

_**上次修改主題的時間：** 2013-03-29_

建立指向 Microsoft Internet Security and Acceleration (ISA) Server 2006 SP1、Forefront Threat Management Gateway 2010 Server 或 Internet Information Server Application Request Routing 之公用外部介面的外部 DNS A 記錄，如 [在 Lync Server 2013 中設定 Edge 支援的 DNS](lync-server-2013-configure-dns-for-edge-support.md) 中所述。您需要每個集區的外部 Web 服務 FQDN、 Director (或 Director 集區)，以及每個簡單 URL 的 DNS 記錄。

必須建立下列記錄，用戶端才能將最少的 DNS 記錄解析到反向 Proxy：

  - 定義 Director 與 Director 集區的已發行外部 Web 服務的主機 (A) 記錄 (例如， **webdirext.contoso.com** )

  - 定義任何 前端集區 與 Standard Edition 伺服器 角色上之外部 Web 服務的已發行外部 Web 服務的主機 (A) 記錄 (例如， **webext.contoso.com** )

  - 簡單 URL 的主機 (A) 記錄 (例如， **dialin.contoso.com** 與 **meet.contoso.com** )

  - Lync Discover External 記錄的主機 (A) 記錄，同時為所有 Web 應用程式提供 AutoDiscover 指標，包含 Lync Web App、排程器與行動力 (例如， **lyncdiscover.contoso.com** )

  - Office Web Apps Server URL 的主機 (A) 記錄 (例如， **officewebapp01.contoso.com** )

如需詳細資訊，請參閱＜[Lync Server 2013 中的 DNS 摘要 - 反向 Proxy](lync-server-2013-dns-summary-reverse-proxy.md)＞。

