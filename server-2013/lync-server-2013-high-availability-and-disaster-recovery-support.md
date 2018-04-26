---
title: Lync Server 2013：高可用性和災害復原支援
TOCTitle: 高可用性和災害復原支援
ms:assetid: 47e77e85-c7c3-4ade-8db7-a34c71aeafd7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204866(v=OCS.15)
ms:contentKeyID: 49290799
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的高可用性和災害復原支援

 

_**上次修改主題的時間：** 2012-09-25_

Lync Server 2013 透過集區以伺服器冗餘方式來提供高可用性。如果執行特定伺服器角色的伺服器失敗，集區中其他執行相同角色的伺服器就會接手該伺服器的負載。這適用於前端伺服器、Edge Server、中繼伺服器和 Director。如需伺服器角色的詳細資訊，請參閱＜ [Lync Server 2013 中的伺服器角色](lync-server-2013-server-roles.md)＞。

Lync Server 2013 也提供災害復原方法，就是啟用集區配對。如果您部署這個拓樸，將會指定前端集區配對，每一對中各個集區都位在不同的資料中心，並且在不同的地理區。如果一個集區或網站故障，您可以重新導向該集區的使用者，以使用該配對中另一個集區，讓服務中斷時間降至最低。

Lync Server 2013 也支援後端伺服器高可用性。這是選用的拓樸，您可在其中為前端集區部署兩部後端伺服器，然後為所有在後端伺服器上執行的 Lync 資料庫設定同步 SQL Server 鏡像。

如需集區配對和後端伺服器鏡像的詳細資訊，請參閱＜ [在 Lync Server 2013 中規劃高可用性和災害復原](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)＞。

## 請參閱

#### 概念

[Lync Server 2013 中的伺服器角色](lync-server-2013-server-roles.md)  
[在 Lync Server 2013 中規劃高可用性和災害復原](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)

