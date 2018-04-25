---
title: Lync Server 2013：適用於 Lync Server 的 Windows 更新
TOCTitle: 適用於 Lync Server 2013 的 Windows 更新
ms:assetid: fe26ab32-b1a9-421d-9227-506703d4b834
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn518337(v=OCS.15)
ms:contentKeyID: 60471203
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 適用於 Lync Server 2013 的 Windows 更新

 

_**上次修改主題的時間：** 2013-12-05_

經常使用 Windows Update Services 檢查並套用更新和安全性更新。這樣做能協助防範其他系統元件中的弱點，避免這些弱點導致攻擊者能夠以系統管理員權限存取執行 Microsoft Lync Server 2013 的伺服器，並因此危害 Lync Server 2013。

Microsoft SQL Server 2008 Express (64 位元版本) 的更新會在每部 Lync Server 2013 Standard Edition Server (針對後端資料庫) 和所有其他 Lync Server 2013 伺服器角色 (針對本機組態存放區) 上執行，除非您已將這些資料庫升級至 SQL Server 2008 R2 Express。您應將這些資料庫，包括前端集區之後端資料庫上的 SQL Server、監控資料庫以及封存資料庫，都視為例行安全性更新維護的一部分。

## 最佳作法

  - 使用 Windows Update 維持最新狀態。

