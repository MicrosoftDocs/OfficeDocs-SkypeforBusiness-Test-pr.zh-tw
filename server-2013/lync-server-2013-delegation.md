---
title: Lync Server 2013：委派
TOCTitle: 委派
ms:assetid: 89e76e5c-3cfb-4504-8d0d-7509c8ba9815
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994045(v=OCS.15)
ms:contentKeyID: 52056143
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的委派

 

_**上次修改主題的時間：** 2013-03-09_

位置基礎路由會對 Lync 中的委派功能有以下類型的影響：

  - 當啟用位置基礎路由的委派代表管理員撥出通話時，委派的語音原則會用於授權通話，且委派的網站語音路由原則將會用於路由傳送通話。

  - 有撥打給管理員的傳入 PSTN 通話時，適用於來電轉接或同時響鈴的規則，也將依照通話與來電轉接和同時響鈴等主題中所述內容套用。

  - 當委派將 PSTN 端點設為同時響鈴目標時，對於撥打給管理員的傳入通話，將會使用與傳入主幹相關聯的網站語音路由原則，將通話路由傳送到委派的 PSTN 端點。

  - 對於委派，建議管理員及其關聯委派應位於相同網站。

## 請參閱

#### 其他資源

[Lync Server 2013 中的位置基礎路由案例](lync-server-2013-scenarios-for-location-based-routing.md)

