---
title: 設定主要管理伺服器
TOCTitle: 設定主要管理伺服器
ms:assetid: 44e2e9a8-c130-4c66-9871-80b1ff11b27c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204844(v=OCS.15)
ms:contentKeyID: 49290764
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定主要管理伺服器

 

_**上次修改主題的時間：** 2014-03-19_

為了充分利用 Microsoft Lync Server 2013 中包含的新運作情況監控功能，系統管理員必須先指定一部電腦作為您的主要管理伺服器；然後您必須在該電腦上安裝 System Center Operations Manager 2007 R2 或 System Center Operations Manager 2012。此外，您必須安裝支援的 SQL Server 版本作為您的 Operations Manager 後端資料庫。如果您是使用 System Center Operations Manager 2012，可以使用下列任何一種版本的 SQL Server 作為您的後端資料庫：

  - SQL Server 2008 R2 Service Pack 1

  - SQL Server 2008 R2 Service Pack 2

如果您是使用 System Center Operations Manager 2007 R2，建議您安裝 SQL Server 2005 Service Pack 4 或 SQL Server 2008 Service Pack 3。您也可以使用 SQL Server 2008 R2 作為 System Center Operations Manager 2007 R2 的後端資料庫。如需將 SQL Server 2008 R2 設定為與 System Center Operations Manager 2007 R2 搭配運作的詳細資訊，請參閱本文件的附錄 1。

當您安裝 System Center Operations Manager 2012 或 System Center Operations Manager 2007 R2 時，必須安裝該產品的所有元件，包括：

  - 操作資料庫

  - 伺服器

  - 主控台

  - Windows PowerShell Cmdlet

  - Web 主控台

  - 報告

  - 資料倉儲

本文件中不會詳細說明這些元件和其安裝。如需 System Center Operations Manager 2007 R2 的詳細資訊，請參閱 Operations Manager 2007 R2 文件，網址為 [http://go.microsoft.com/fwlink/?linkid=257526\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=257526%26clcid=0x404)，以及 System Center Operations Manager 2012 文件，網址為 [http://go.microsoft.com/fwlink/?linkid=257527\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=257527%26clcid=0x404)。如果您要使用 SQL Server 2005 或 SQL Server 2008 Service Pack 1 作為您的後端資料庫，應依照這些指示進行。

如果您是使用 System Center Operations Manager 2012，可以使用 SQL Server 2012 作為您的後端資料庫。如需 SQL Server 2012 的詳細資訊，請參閱 SQL Server 2012 線上叢書，網址為 [http://go.microsoft.com/fwlink/?linkid=257528\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=257528%26clcid=0x404)。

請記住，每個 Lync Server 部署只能有一部「主要管理伺服器」。此外，雖然您可以使用 System Center Operations Manager 2012 或 System Center Operations Manager 2007 R2，但是您無法同時執行兩個應用程式；您必須選擇其中之一。例如，如果您是執行 System Center Operations Manager 2012，則您所有的 System Center 代理程式也必須執行 System Center Operations Manager 2012。您不可以讓部分代理程式執行 System Center Operations Manager 2012，而讓其他的代理程式執行 System Center Operations Manager 2007 R2。

