---
title: Lync Server 2013：支援通話駐留的用戶端
TOCTitle: 支援通話駐留的用戶端
ms:assetid: c236d2ba-9d83-418c-9cbc-92541f115fb0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412958(v=OCS.15)
ms:contentKeyID: 49292213
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中支援通話駐留的用戶端

 

_**上次修改主題的時間：** 2012-09-13_

本節識別可用於駐留通話的用戶端，以及可用於擷取駐留之通話的用戶端。

## 駐留通話支援的用戶端

您可以駐留來自任何 IP、專用交換機 (PBX)、公用交換電話網路 (PSTN) 或行動電話的通話。

> [!NOTE]  
> 只可以駐留音訊通話。不能駐留立即訊息和會議。



下列用戶端可以使用 通話駐留 來駐留通話：

  - Lync 2013

  - Lync 2010

  - Lync 2010 Attendant

  - Lync Phone Edition

> [!NOTE]  
> 行動電話無法使用 通話駐留 來駐留通話。



## 擷取通話支援的用戶端

軌道範圍是設定為虛擬分機區塊 (未指派使用者或電話的分機)。將軌道設定為虛擬分機時，行動電話和 PSTN 電話就無法擷取駐留的通話。

同盟使用者無法擷取駐留的通話。

下列用戶端可以擷取駐留在 通話駐留 上的通話：

  - Lync 2013

  - Lync 2010

  - Lync 2010 Attendant

  - Lync Phone Edition

  - IP 公用區電話

  - 連接至 Lync Server 2013 基礎結構的非 IP 電話，包括公用區電話和專用交換機 (PBX) 電話

