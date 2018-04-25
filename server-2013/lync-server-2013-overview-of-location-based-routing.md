---
title: Lync Server 2013：位置基礎路由概觀
TOCTitle: 位置基礎路由概觀
ms:assetid: 4aa494bd-0d66-4335-b9e8-f758d44a7202
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994032(v=OCS.15)
ms:contentKeyID: 52056101
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的位置基礎路由概觀

 

_**上次修改主題的時間：** 2013-02-21_

以位置為基礎的路由引進一組新規則集，可修改國家和國際 PSTN 電話的路由來禁止 PSTN 免話費機制。以位置為基礎的路由可讓您針對特定的地區、特定的閘道或僅限特定的使用者集，靈活調整這些規則的範圍。

下列案例說明以位置為基礎的路由可能強制執行的主要限制類型：

  - 輸出通話 – 以位置為基礎的路由可從來電者所在的相同地區中的 PSTN 閘道，強制輸出「輸出電話」以禁止 PSTN 免話費機制，從而禁止從非來電者的所在地區的 PSTN 閘道輸出電話。

  - 接收通話 – 如果 PSTN 閘道路由的來電不是來自撥打的 Lync 使用者所在的相同地區，以位置為基礎的路由可禁止 PSTN 來電在 Lync 端點發出鈴響。

  - 未知地區 – 以位置為基礎的路由可限制與未確定位置的使用者之間所進行的撥入和撥出 PSTN 通話 (例如，從網際網路連線的遠端使用者，或位於不明地區的使用者)。

  - 國際地區 – 如果在使用者所在的地區找不到本機閘道，以位置為基礎的路由會透過國際 PSTN 閘道來強制路由撥出通話。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中規劃位置基礎路由](lync-server-2013-planning-for-location-based-routing.md)

