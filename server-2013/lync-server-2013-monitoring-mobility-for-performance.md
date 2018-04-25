---
title: 在 Lync Server 2013 中針對效能監控行動性
TOCTitle: 在 Lync Server 2013 中針對效能監控行動性
ms:assetid: 9c831c63-9a7d-48ec-9118-f8a7e80ddd04
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690033(v=OCS.15)
ms:contentKeyID: 49291804
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中針對效能監控行動性

 

_**上次修改主題的時間：** 2013-02-14_

Lync Server Mobility Service 會增加前端伺服器和前端集區上的負載。若行動裝置 (例如 Android 和 Nokia 裝置) 在行動應用程式最小化時仍維持與伺服器連線，則其負載會比在行動應用程式最小化時終止與伺服器連線的裝置來得大。當行動使用量增加時，您必須監控行動效能以判斷何時需要增加容量。

有多個限制會影響行動效能：

  - 可用的記憶體

  - 要求佇列限制

  - 同時連線數目

  - IIS 佇列長度

在伺服器上可影響行動效能的其他限制包括十二個同時登入、驗證，以及工作階段更新和終止的最大值。大多數的部署不需要修改這些最大值。

## 本章節內容

  - [監控伺服器記憶體容量限制](lync-server-2013-monitoring-for-server-memory-capacity-limits.md)

  - [監控 Mobility Service 與 UCWA 使用方式](lync-server-2013-monitoring-mobility-service-and-ucwa-usage.md)

  - [設定高效能的 Mobility Service](lync-server-2013-configuring-mobility-service-for-high-performance.md)

  - [監控 IIS 要求的追蹤記錄檔](lync-server-2013-monitoring-iis-request-tracing-log-files.md)

  - [行動效能計數器](lync-server-2013-mobility-performance-counters.md)

