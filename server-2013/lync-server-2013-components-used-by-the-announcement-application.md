---
title: Lync Server 2013：宣告應用程式所使用的元件
TOCTitle: 宣告應用程式所使用的元件
ms:assetid: 7b1a0281-cf31-459d-a734-5f10a129089c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398608(v=OCS.15)
ms:contentKeyID: 49291408
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的宣告應用程式所使用的元件

 

_**上次修改主題的時間：** 2012-09-13_

在 Lync Server 2013 中， 宣告應用程式是 回應群組應用程式的一項元件。當您部署 企業語音時， 宣告應用程式會自動隨 回應群組應用程式安裝並啟動。本節將說明支援 宣告應用程式的元件。

## 宣告應用程式元件

以下是支援 Lync Server的 宣告應用程式 元件：

  - **應用程式服務**    應用程式服務可提供用以部署、裝載及管理整合通訊應用程式的平台。 應用程式服務 會自動安裝在 前端集區中的每一部前端伺服器上，以及每一部 Standard Edition Server 上。

  - **回應群組應用程式**    回應群組應用程式是 應用程式服務所主控的整合通訊應用程式之一。將未指派的電話號碼範圍設定成要路由至宣告後，需要有 回應群組應用程式來路由撥給該電話號碼的電話。(如果所有範圍都設定成要路由至 Exchange Unified Messaging (UM)，則不需要有 回應群組應用程式。)

  - **音訊檔**   音訊檔可用於宣告。

  - **檔案存放區**    宣告應用程式會使用檔案存放區儲存其音訊檔。

  - **Lync Server 控制台**   您可以使用 Lync Server 控制台設定未指派號碼表格。

  - **Lync Server 管理命令介面**   您可以使用 Lync Server 管理命令介面 Cmdlet 來設定宣告設定和未指派號碼表格。

