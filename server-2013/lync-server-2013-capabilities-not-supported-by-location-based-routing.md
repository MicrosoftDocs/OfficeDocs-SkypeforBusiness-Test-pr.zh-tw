---
title: Lync Server 2013：未受位置基礎路由支援的功能
TOCTitle: 未受位置基礎路由支援的功能
ms:assetid: c3d54953-a7d6-4465-a6c3-ae411b2d8ea9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994071(v=OCS.15)
ms:contentKeyID: 52056219
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中未受位置基礎路由支援的功能

 

_**上次修改主題的時間：** 2014-03-12_

以位置為基礎的路由並不適用於下列類型的互動。當 Lync 端點使用這些功能與 PSTN 端點互動時，並不會強制執行以位置為基礎的路由。

  - PSTN 撥入會議

  - 透過回應群組來電與撥出的 PSTN 電話

  - 通話保留或透過通話保留擷取的 PSTN 電話

  - 撥入宣告服務的 PSTN 來電

  - 透過群組來電接聽擷取的 PSTN 來電

若要對下列清單中的互動類型強制執行以位置為基礎的路由規則，您必須針對會議啟用以位置為基礎的路由：

  - 從會議撥出的 PSTN

  - 從對等音訊交談擴大到牽涉 PSTN 端點的會議

  - 牽涉 PSTN 端點的諮詢轉接

若要針對會議啟用以位置為基礎的路由，請參閱 [會議位置基礎路由](lync-server-2013-location-based-routing-for-conferencing.md)。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中規劃位置基礎路由](lync-server-2013-planning-for-location-based-routing.md)

