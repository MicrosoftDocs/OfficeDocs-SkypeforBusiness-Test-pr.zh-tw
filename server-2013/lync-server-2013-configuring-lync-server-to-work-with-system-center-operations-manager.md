---
title: 設定 Lync Server 以搭配 System Center Operations Manager 使用
TOCTitle: 設定 Lync Server 以搭配 System Center Operations Manager 使用
ms:assetid: b55a24ab-648b-4142-b3cd-3792860ba872
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205188(v=OCS.15)
ms:contentKeyID: 49292067
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Lync Server 以搭配 System Center Operations Manager 使用

 

_**上次修改主題的時間：** 2012-10-22_

為了設定 Microsoft Lync Server 2013 基礎結構與 System Center Operations Manager 搭配使用，您必須進行下列三個動作：

  - 識別並設定主要 System Center Operations Manager 管理伺服器。設定管理伺服器包含安裝 System Center Operations Manager 2012 或 System Center Operations Manager 2007 R2，以及使用 SQL Server 來設定後端資料庫。您需要的 SQL Server 確切版本根據使用的 System Center Operations Manager 而定。如需詳細資訊，請參閱[設定主要管理伺服器](lync-server-2013-configuring-the-primary-management-server.md)。

  - 識別與設定您要監視 Lync Server 電腦。若要使用 System Center Operations Manager 來監視 Lync Server 電腦，您必須安裝 System Center Operations Manager 代理檔案，然後將每部伺服器設定為 Pproxy。

  - 識別與設定您要當作 Lync Server 「監看員節點」的電腦。監看員節點是會定期執行 Lync Server 綜合交易的電腦，也是可驗證主要 Lync Server 元件的 Windows PowerShell Cmdlet，如登入系統的功能或交換即時訊息的功能如預期運作。

本章節中的主題包含執行下列每一項工作的指示。

## 本節內容

  - [設定主要管理伺服器](lync-server-2013-configuring-the-primary-management-server.md)

  - [安裝 Lync Server 2013 管理套件](lync-server-2013-installing-the-lync-server-2013-management-packs.md)

  - [設定要監控的 Lync Server 電腦](lync-server-2013-configuring-the-lync-server-computers-that-will-be-monitored.md)

  - [安裝和設定監看員節點](lync-server-2013-installing-and-configuring-watcher-nodes.md)

