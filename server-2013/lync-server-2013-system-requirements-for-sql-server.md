---
title: Lync Server 2013：SQL Server 的系統需求
TOCTitle: SQL Server 的系統需求
ms:assetid: 9c235085-cbfa-4e9e-9cec-3f5749039a6b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205112(v=OCS.15)
ms:contentKeyID: 49291793
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中 SQL Server 的系統需求

 

_**上次修改主題的時間：** 2013-10-25_

在部署 Enterprise Edition Server 之前，請在符合硬體需求的專用電腦上安裝 Microsoft SQL Server 2008 R2 或 Microsoft SQL Server 2012。如需硬體需求的詳細資訊，請參閱＜支援＞文件中的 [Lync Server 2013 的伺服器硬體平台](lync-server-2013-server-hardware-platforms.md)。如需軟體需求的詳細資訊，請參閱＜支援＞文件中的 [Lync Server 2013 中的資料庫軟體支援](lync-server-2013-database-software-support.md)。如需部署所需權限的相關資訊，請參閱 [Lync Server 2013 中 SQL Server 的部署權限](lync-server-2013-deployment-permissions-for-sql-server.md)。

在建立前端集區之前，您還必須設定 Windows 防火牆允許 Lync Server 2013 透過特定連接埠存取 SQL Server，方法是使用 SQL Server 組態管理員來定義伺服器的連接埠，然後在具有進階安全性的 Windows 防火牆中開啟這些連接埠。

