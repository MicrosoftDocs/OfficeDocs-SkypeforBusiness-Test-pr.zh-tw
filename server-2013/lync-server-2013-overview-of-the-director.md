---
title: Lync Server 2013：Director 概觀
TOCTitle: Director 概觀
ms:assetid: cf9919b3-e16b-47c5-be1d-2c4bc64f44ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398879(v=OCS.15)
ms:contentKeyID: 49292370
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Director 概觀

 

_**上次修改主題的時間：** 2012-09-08_

Director 是執行 Lync Server 2013 的伺服器，用於驗證使用者要求，但不裝載任何使用者。您可以在下列兩個案例中選用部署 Director：

  - 如果您部署 Edge Server 以讓外部使用者可進行存取，那麼也應該部署 Director。在此案例中， Director 會驗證外部使用者，然後將其流量傳遞至內部伺服器。當使用 Director 來驗證外部使用者時，會免除 前端集區伺服器執行驗證這些使用者之作業的負擔。此外，也有助於為內部 前端集區隔離惡意流量，例如拒絕服務攻擊。如果網路上因此類攻擊而充斥無效的外部流量，這些流量將止於 Director。

  - 如果您在中央網站部署了多個 前端集區，可透過將 Director 新增至該網站來簡化驗證要求並改善效能。在此案例中，所有要求會先送到 Director，然後 Director 會將這些要求路由傳送到正確的 前端集區。

