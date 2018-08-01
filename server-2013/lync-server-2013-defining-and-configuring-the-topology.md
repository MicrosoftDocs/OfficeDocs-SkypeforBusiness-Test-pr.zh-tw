---
title: Lync Server 2013：定義和設定拓撲
TOCTitle: 定義和設定拓撲
ms:assetid: 51d1601e-4f83-48d4-ad08-3b4d5e2003aa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398339(v=OCS.15)
ms:contentKeyID: 49290913
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中定義和設定拓撲

 

_**上次修改主題的時間：** 2012-09-14_

您可以使用 拓撲產生器定義與設定拓撲。使用 拓撲產生器時，您不需要是本機 Administrators 群組或是有權限的網域群組 (例如 Domain Admins) 的成員。您可以標準使用者身分定義拓撲。當您在第一次使用與後續編輯工作階段中啟動 拓撲產生器時，系統會提示您輸入希望 拓撲產生器載入目前組態文件的位置。選項如下：

  - 從現有部署下載拓撲

  - 從本機檔案開啟拓撲

  - 新增拓撲

如果您已經定義拓撲，並且建立了 中央管理存放區，則您應該選擇從現有部署下載拓撲。 拓撲產生器將會讀取資料庫並擷取目前定義。如果您已有 中央管理存放區，請一律選擇這個選項。

如果您尚未建立 中央管理存放區，而且想要編輯先前儲存的組態，則您應該開啟本機檔案裡的拓撲。您將開啟的檔案，必須是先前工作階段中儲存的組態檔。您可以透過這個選項，編輯先前儲存的拓撲。

> [!WARNING]
> 如果您已經有發行的拓撲，請勿載入本機組態檔。您應該選擇從現有部署下載拓撲。


如果您想要建立新的 拓撲產生器組態，請選擇建立新的拓撲。除非您選擇將先前儲存的設計儲存您在先前設計工作階段裡建立的相同檔案，否則不會複寫先前儲存的設計。

在下列每個選項當中，系統會提示您輸入要用來儲存 拓撲產生器組態檔的位置。該檔案位置可以是本機位置、已建立的檔案共用之共用位置，或是卸除式媒體。

## 本章節內容

  - [針對 Lync Server 2013 在拓撲建置器中定義和設定拓撲](lync-server-2013-define-and-configure-a-topology-in-topology-builder.md)

  - [在 Lync Server 2013 中定義和設定前端集區或 Standard Edition Server](lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md)

  - [在 Lync Server 2013 中針對災害復原部署配對前端集區](lync-server-2013-deploying-paired-front-end-pools-for-disaster-recovery.md)

  - [在 Lync Server 2013 中針對後端伺服器高可用性部署 SQL 鏡像](lync-server-2013-deploying-sql-mirroring-for-back-end-server-high-availability.md)

  - [在 Lync Server 2013 中編輯或設定簡單 URL](lync-server-2013-edit-or-configure-simple-urls.md)

  - [在 Lync Server 2013 中選取中央管理伺服器](lync-server-2013-select-the-central-management-server.md)

