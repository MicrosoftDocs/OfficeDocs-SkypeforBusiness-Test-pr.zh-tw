---
title: 設定封存的儲存
TOCTitle: 設定封存的儲存
ms:assetid: f751245c-743e-454f-8325-968ae5e3de71
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205392(v=OCS.15)
ms:contentKeyID: 49292848
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定封存的儲存

 

_**上次修改主題的時間：** 2013-12-17_

Lync Server 2013 的封存儲存區包含下列項目：

  - **資料存放區**   必須有資料存放區才能儲存 IM 內容。

  - **檔案存放區**   必須有檔案存放區才能儲存會議內容資料存放區和檔案存放區。

## 設定資料存放區

「在 Lync Server 2013 中封存」的設定資料存放區的必要條件，需視您要封存資料的方式而定：

  - 整合 Lync Server 2013使用 Exchange 部署封存以儲存使用 Exchange 存放區的封存資料

  - 設定另一個 SQL Server 資料庫伺服器以儲存封存資料。

## 設定用於封存資料的 Exchange 存放區

若要設定用於封存資料存放區的 Exchange，您的 Exchange 部署必須正在執行 Exchange 2013。此外，使用者信箱必須位於 Exchange 2013 伺服器上，且他們的信箱必須放置於 \[就地保留\] 上。如需設定 Exchange 2013 的詳細資訊，請參閱 Exchange 產品說明文件。

## 設定用於封存資料存放區的 SQL Server 資料庫伺服器

「在 Lync Server 2013 封存」必須由 SQL Server 資料庫軟體儲存封存的資料，除非您使用 Exchange 部署來整合。.

若要由 SQL Server 封存資料庫，您必須在有封存資料庫的電腦上安裝 SQL Server。您可以使用做為「前端」集區的後端資料庫的相同 SQL 實例。若要有最佳效能，您應該將封存資料庫部署至與中央管理存放區不同的電腦上。如需組合 Lync Server 2013 元件的詳細資訊，請參閱「支援能力」說明文件中的 [Lync Server 2013 中支援的伺服器組合](lync-server-2013-supported-server-collocation.md) 。

每部資料庫伺服器都必須執行 SQL Server 的支援版本。如需支援版本的詳細資料，請參閱「規劃」說明文件中的 [Lync Server 2013 中封存的技術需求](lync-server-2013-technical-requirements-for-archiving.md)。

您必須先設定 SQL Server 平台才能部署和啟用封存功能。如果用來發佈拓撲的帳戶擁有適當的系統管理員權限，您可以在發佈拓撲時建立封存資料庫 (LcsLog)。您也可以稍後建立資料庫，這是安裝程序的一部分。如需 SQL Server 的詳細資訊，請參閱 SQL Server TechCenter，網址為：[http://go.microsoft.com/fwlink/?linkid=129045\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=129045%26clcid=0x404)。

> [!NOTE]  
> 確認 SQL Server Agent 服務的 [啟動類型] 為 [自動]，且 SQL Server Agent 服務正針對擁有封存資料庫的 SQL 執行個體執行中，以便預設封存 SQL Server 維護工作可在 SQL Server Agent 服務的控制下按其排程執行。



## 設定檔案存放區

當您設定了「前端」集區或 Standard Edition 伺服器，封存會使用 Lync Server 2013 您指定的檔案共用。您無法變更用於封存的檔案共用。如需支援的檔案存放區系統詳細資訊，請參閱「支援能力」說明文件中的 [Lync Server 2013 中的檔案儲存支援](lync-server-2013-file-storage-support.md)。

