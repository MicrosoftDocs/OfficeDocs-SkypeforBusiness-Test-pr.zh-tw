---
title: Lync Server 2013 中的音訊/視訊 (A/V) Edge Server
TOCTitle: Lync Server 2013 中的音訊/視訊 (A/V) Edge Server
ms:assetid: b0cc538b-77eb-47fb-be82-5ab0631c6219
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721852(v=OCS.15)
ms:contentKeyID: 49890261
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的音訊/視訊 (A/V) Edge Server

 

_**上次修改主題的時間：** 2012-11-01_

A/V Edge Service 提供方法讓您的內部使用者 (登入您組織網路的使用者) 能與外部使用者 (未登入您組織網路的使用者) 共用音訊與視訊。除了音訊與視訊之外，A/V Edge 服務也提供桌面共用與檔案傳輸的支援。

A/V Edge Service 主要是使用 A/V Edge 設定來進行管理；這些設定可讓您管理分配到每個連接埠與每位使用者的頻寬上限，並讓您指定在更新驗證 Token 前可使用驗證 Token 的時間長短。A/V Edge 組態設定可套用至網站或個別 A/V Edge Server。在決定設定集合的優先順序時，請使用下列指南：

  - 服務範圍上的設定 (也就是個別伺服器) 優先順序最高。

  - 網站範圍上的設定優先順序高於全域範圍上的設定。不過，服務範圍設定會取代網站範圍設定。

  - 只有在個別伺服器上沒有服務設定，以及伺服器所在的網站上沒有網站設定時，才會使用全域範圍的設定。

只能使用 Lync Server PowerShell 與 CsAVEdgeConfiguration Cmdlet 來管理 A/V Edge Service。

## 本章節內容

  - [傳回 A/V Edge Server 設定資訊](lync-server-2013-return-a-v-edge-server-configuration-information.md)

  - [建立或修改 A/V Edge Server 的組態設定集合](lync-server-2013-create-or-modify-a-collection-of-a-v-edge-server-configuration-settings.md)

  - [刪除現有的 A/V Edge Server 組態設定集合](lync-server-2013-delete-an-existing-collection-of-a-v-edge-server-configuration-settings.md)

