---
title: Lync Server 2013：通話駐留所使用的元件
TOCTitle: 通話駐留所使用的元件
ms:assetid: c7ffbee3-0ce1-48c0-bb56-af098b41d6d6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398824(v=OCS.15)
ms:contentKeyID: 49292299
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中通話駐留所使用的元件

 

_**上次修改主題的時間：** 2012-09-13_

通話駐留應用程式會在您部署 Enterprise Voice 時自動安裝。您可以透過設定語音原則來啟用 通話駐留。以下是支援 通話駐留應用程式的 Lync Server 2013 元件：

  - **應用程式服務**    應用程式服務提供部署、裝載和管理整合通訊應用程式的平台，例如 通話駐留應用程式。 應用程式服務會自動安裝在 前端集區中的每部前端伺服器上，以及每部 Standard Edition Server 上。

  - **通話駐留應用程式**    通話駐留應用程式是 應用程式服務所主控的整合通訊應用程式之一。它會在您部署 Enterprise Voice 時自動包含在內。 通話駐留會駐留並擷取通話，以及管理通話駐留軌道。

  - **等候音樂檔案**   如果已啟用音樂，則會在通話駐留時播放音樂檔案。安裝 通話駐留應用程式時會隨附預設音樂檔案。

  - **檔案存放區**    通話駐留應用程式會使用檔案存放區來保留自訂音訊檔案。

  - **Lync Server 控制台**   您可以使用 Lync Server 控制台來設定通話駐留軌道表，並為使用者啟用 通話駐留。

  - **Lync Server 管理命令介面**   所有 通話駐留應用程式設定都能使用 Lync Server 管理命令介面 Cmdlet 來執行。

