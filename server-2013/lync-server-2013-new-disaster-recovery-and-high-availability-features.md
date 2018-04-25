---
title: Lync Server 2013：新的災害復原和高可用性功能
TOCTitle: 新的災害復原和高可用性功能
ms:assetid: 4fa7cd0f-784b-4d3f-b839-432c2ecaf7c1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204892(v=OCS.15)
ms:contentKeyID: 49290886
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中新的災害復原和高可用性功能

 

_**上次修改主題的時間：** 2012-09-20_

如同在 Lync Server 2010 中， Lync Server 2013 主要的高可用性 (HA) 配置是以透過集區提供的伺服器備援為基礎。如果執行特定伺服器角色的伺服器失敗，集區中執行相同角色的其他伺服器就會接手該伺服器的負載。這適用於前端伺服器、Edge Server、中繼伺服器和 Director。

Lync Server 2013 新增了災害復原的方法，就是讓您可以為兩個資料中心內的前端集區配對。如果配對的集區中有一個故障，系統管理員可以將使用者從該集區容錯移轉至配對中的另一個集區，以便繼續提供服務。這項功能不需要昂貴的網路或硬體解決方案，例如存放網路或共用磁碟。

Lync Server 2013 也新增了後端伺服器高可用性。這是一個選用的拓樸，您可在其中為前端集區部署兩個後端伺服器，然後為在後端伺服器上執行的所有 Lync 資料庫設定同步 SQL 鏡像。您可以選擇是否要部署鏡像見證。

## 請參閱

#### 概念

[在 Lync Server 2013 中規劃高可用性和災害復原](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)

