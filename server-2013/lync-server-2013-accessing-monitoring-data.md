---
title: 在 Lync Server 2013 中存取監控資料
TOCTitle: 在 Lync Server 2013 中存取監控資料
ms:assetid: 845385ca-5532-4fa2-91b9-51c6de6fec91
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688116(v=OCS.15)
ms:contentKeyID: 49890149
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中存取監控資料

 

_**上次修改主題的時間：** 2012-09-05_

監視資料儲存於以兩個為一組的 SQL Server 資料庫：LcsCdr 儲存詳細通話記錄資料，QoEMetrics 儲存經驗品質資料。這兩個資料庫沒有特別規定，這表示，使用您一般用來存取和分析 SQL Server 資料庫所用的任何工具，即可存取這些資料庫中儲存的資料。

存取和分析監視資料時，您應該考慮使用的一個工具是 Lync Server 監視報告。監視報告是一組由 Microsoft SQL Server Reporting Services 所發行的標準報告。使用網頁瀏覽器即可存取這些報告，其中提供使用情形、通話診斷資訊及媒體品質資訊，所有內容均是以 CDR 及 QoE 資料庫中儲存的詳細通話記錄 (CDR) 及經驗品質 (QoE) 記錄為依據。監視報告由 Lync Server 2013 提供，可在安裝 Lync Server 並設定監視之後從 Lync Server 部署精靈安裝。

請注意，監視報告需要使用 SQL Server Reporting Service。安裝 SQL Server 時，可同時安裝 SQL Server Reporting Service，也可在安裝 SQL Server 之後隨時安裝。

如需詳細資訊，請參閱《Lync Server 2013 部署指南》中的主題＜[安裝 Lync Server 2013 監控報告](lync-server-2013-installing-lync-server-2013-monitoring-reports.md)＞。

