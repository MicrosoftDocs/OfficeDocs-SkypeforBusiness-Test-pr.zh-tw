---
title: 設定系統平台進行封存
TOCTitle: 設定系統平台進行封存
ms:assetid: 2df40fdf-0e32-46d4-9fb2-1ce1d7bfa328
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204768(v=OCS.15)
ms:contentKeyID: 49290453
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定系統平台進行封存

 

_**上次修改主題的時間：** 2012-10-09_

開始部署封裝之前，必須先在符合系統需求的硬體上安裝所需作業系統，以及所有先決條件軟體。

  - **Lync Server 2013 平台**   Lync Server 2013 部署並無封存伺服器。但在前端伺服器及 Standard Edition Server 上執行的整合資料收集代理程式會擷取封裝的資料，因此不需要使用另一個系統平台主控封裝。

  - **資料儲存平台**   在 Lync Server 2013 中，您可使用下列方式之一儲存資料：
    
      - **Microsoft Exchange 整合**   若您要使用 Exchange 2013 部署儲存 Lync Server 2013 封裝資料，而不是透過設定另一個資料庫以儲存封裝資料的方式，則您的 Exchange 部署必須執行 Exchange 2013。如需設定 Exchange 2013 系統平台的詳細資訊，請參閱 Exchange 產品文件。
    
      - **SQL Server**   若您要使用另一個 SQL Server 資料庫儲存封裝資料，而不是使用 Microsoft Exchange 整合，就必須先設定資料庫的系統平台，再部署封裝。此特定系統平台需求會根據您是為封裝資料庫使用 Microsoft SQL Server 2008 R2 或 Microsoft SQL Server 2012 而有所不同。如需為這些資料庫設定系統平台的詳細資訊，請參閱 Microsoft SQL Server 2008 R2 及 Microsoft SQL Server 2012 產品文件。

  - **檔案伺服器平台**   Lync Server 2013 會將 Lync Server 封裝檔案儲存在您設定前端伺服器或 Standard Edition Server 時，為檔案儲存所指定的相同位置中 。您無法指定另一個封裝檔案儲存的位置，所以也不需要另一個封裝檔案儲存的系統平台。若您使用 Microsoft Exchange 整合，封裝的 Lync 通訊 Exchange 2013 檔案會針對位於 Exchange 伺服器的使用者儲存在 Exchange 2013 伺服器。

