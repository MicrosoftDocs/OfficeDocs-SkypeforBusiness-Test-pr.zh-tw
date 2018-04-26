---
title: Lync Server 2013：用於監控的元件與拓撲
TOCTitle: 用於監控的元件與拓撲
ms:assetid: c1bb36b0-1fb8-4d8e-9cc9-9bef740fe3c6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412952(v=OCS.15)
ms:contentKeyID: 49890291
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中用於監控的元件與拓撲

 

_**上次修改主題的時間：** 2012-09-05_

由於每部前端伺服器上都會自動安裝並啟動整合資料收集代理程式，因此您無需設定要做為監控伺服器的伺服器；每部前端伺服器都已具備監控伺服器的功能。不過，您仍需安裝並設定要做為監控資料之後端資料存放區的資料庫。 Microsoft Lync Server 2013 可以使用下列任何資料庫做為監控所需的後端存放區：

  - Microsoft SQL Server 2008 R2 Enterprise Edition

  - Microsoft SQL Server 2008 R2 Standard Edition

  - Microsoft SQL Server 2012 Enterprise Edition

  - Microsoft SQL Server 2012 Standard Edition

請注意，您必須使用這些資料庫的 64 位元版本；32 位元版本 SQL Server 無法當做監控的後端存放區使用。同樣地， Lync Server 2013 不支援 SQL Server 2008 或 SQL Server 2012 的 Express Edition。如需 Lync Server 2013 資料庫需求的詳細資訊，請參閱《 Lync Server 2013 支援》指南的 [Lync Server 2013 中的資料庫軟體支援](lync-server-2013-database-software-support.md)主題。

請記住，您必須在部署和設定監控前，先安裝和設定 SQL Server。但您只需要部署 SQL Server 本身，不需要預先安裝監控資料庫，這些資料庫會在您發行 Lync Server 拓撲時自動建立。

監控資料可與其他類型的資料共用一個 SQL Server 執行個體。一般來說，詳細通話記錄資料庫 (LcsCdr) 和經驗品質資料庫 (QoEMetrics) 會共用同一個 SQL 執行個體，而兩個監控資料庫通常會跟封存資料庫 (LcsLog) 位於同一個 SQL 執行個體。對於 SQL Server 執行個體的唯一真正需求，大概就是任何一個 SQL Server 執行個體都限採用下列項目：

  - 一個 Lync Server 2013 後端資料庫執行個體 (通常來說，不建議將監控資料庫置於與後端資料庫相同的 SQL 執行個體中，或甚至相同的電腦上。雖然技術上是可以這樣做，但可能會有監控資料庫用掉後端資料庫所需磁碟空間的風險)。

  - 一個詳細通話記錄資料庫執行個體。

  - 一個經驗品質資料庫執行個體。

  - 一個封存資料庫執行個體。

換句話說，在同一個 SQL Server 執行個體中不能同時有兩個 LcsCdr 資料庫執行個體。如果您需要多個 LcsCdr 資料庫執行個體，則需要設定多個 SQL Server 執行個體。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中部署監控](lync-server-2013-deploying-monitoring.md)

