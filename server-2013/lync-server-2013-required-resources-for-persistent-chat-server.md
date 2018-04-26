---
title: Lync Server 2013：常設聊天室伺服器的必要資源
TOCTitle: 必要資源
ms:assetid: bce50b95-f3c8-407e-963a-d8896ee77fbc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205211(v=OCS.15)
ms:contentKeyID: 49292140
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的常設聊天室伺服器的必要資源

 

_**上次修改主題的時間：** 2013-11-01_

常設聊天室伺服器 的高可用性和災害復原功能所需要的資源，超過全面運作的一般需求。在設定 常設聊天室伺服器 的高可用性和災害復原前，請確定除了標準 常設聊天室伺服器 運作的需求以外，您還具備下列資源。如需詳細的設定資訊，請參閱＜ [在 Lync Server 2013 中設定常設聊天室伺服器](lync-server-2013-configuring-persistent-chat-server.md)＞(可能為英文網頁)。

  - 一個專用的資料庫執行個體，位於 常設聊天室伺服器 服務之主前端所在的同一個實體資料中心上。此資料庫將做為主要 常設聊天室 資料庫的 SQL Server 鏡像。如果您希望可以自動容錯移轉至鏡像資料庫，則可選擇指定其他 SQL Server 做為鏡像見證。

  - 一個位於其他實體資料中新的專用資料庫執行個體。這個資料庫將做為主要資料中心之資料庫的 SQL Server 記錄傳送次要資料庫。

  - 一個專用的資料庫執行個體，做為次要資料庫的 SQL Server 鏡像。可選擇指定其他 SQL Server 做為鏡像見證。這些資料庫都必須位於次要資料庫的同一個實體資料中心上。

  - 如果啟用 常設聊天室伺服器 規範，則需要另外三個專用的資料庫執行個體。其分佈與先前概述的 常設聊天室 資料庫相同。如果規範資料庫可與 常設聊天室 資料庫共用相同的 SQL Server 執行個體，則建議針對高可用性和災害復原採用獨立執行個體。

  - 必須為 SQL Server 記錄傳送交易記錄檔建立和指定檔案共用。在兩個資料中心內執行 常設聊天室 資料庫的的所有 SQL 伺服器，對於此檔案共用必須具備讀/寫權限。此共用並未定義為 FileStore 角色的一部分。

  - 次要資料庫伺服器上的檔案共用，做為主要伺服器檔案共用之 SQL Server 交易記錄檔的複製目的資料夾。

下圖提供在兩個不同的延伸集區拓撲中設定整體 Persistent Chat Server 集區 的範例方法：

  - 資料中心有實際地理位置，且具備高頻寬/低延遲的延伸 Persistent Chat Server 集區。

  - 資料中心有實際地理位置，且具備低頻寬/高延遲的延伸 Persistent Chat Server 集區。

下圖顯示資料中心有實際地理位置，且具備高頻寬/低延遲的延伸 Persistent Chat Server 集區拓撲。

**資料中心有實際地理位置，且具備高頻寬/低延遲的延伸 Persistent Chat Server 集區。**

![Persistent Chat Server 集區 HBW 組態範例](images/JJ205211.55d10910-c824-41e6-bed2-08d13a2abd65(OCS.15).jpg "Persistent Chat Server 集區 HBW 組態範例")

下圖顯示資料中心有實際地理位置，且具備低頻寬/高延遲的延伸 Persistent Chat Server 集區拓撲。

**資料中心有實際地理位置，且具備低頻寬/高延遲的延伸 Persistent Chat Server 集區。**

![Persistent Chat Server 集區 LBW 組態範例](images/JJ205211.586b0a3a-3767-4991-944f-ee54389512aa(OCS.15).jpg "Persistent Chat Server 集區 LBW 組態範例")

