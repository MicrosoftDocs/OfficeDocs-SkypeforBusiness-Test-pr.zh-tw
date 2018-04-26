---
title: Lync Server 2013：位置基礎路由的技術考量
TOCTitle: 位置基礎路由的技術考量
ms:assetid: 2e2a9199-7c6f-48d3-9adb-3873fc4f8c4e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994027(v=OCS.15)
ms:contentKeyID: 52056080
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的位置基礎路由的技術考量

 

_**上次修改主題的時間：** 2013-03-09_

規劃位置基礎路由時，您應考量可能於下列情況發生的影響。

## 災害復原

在從主要集區轉移到備份集區的容錯移轉，以及將一般作業還原到主要集區時，位置基礎路由會於災害復原程序期間始終維持執行。

## Survivable Branch Appliance

設定位置基礎路由會影響部署 Survivable Branch Appliance 關聯閘道的位置規劃。SBA 關聯閘道必須和 Survivable Branch Appliance 位於相同網站；否則，如果設定了位置基礎路由，位於您 Survivable Branch Appliance 上的使用者將無法撥打輸出通話。當 Survivable Branch Appliance 和中央網站之間的 WAN 連線故障時，位置基礎路由限制會維持執行。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中規劃位置基礎路由](lync-server-2013-planning-for-location-based-routing.md)

