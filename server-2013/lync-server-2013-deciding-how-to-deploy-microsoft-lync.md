---
title: Lync Server 2013：決定 Microsoft Lync 的部署方式
TOCTitle: 決定 Microsoft Lync 的部署方式
ms:assetid: 6ca677d3-745d-4935-8f05-19274a8bccf2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204979(v=OCS.15)
ms:contentKeyID: 49291233
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 決定 Lync Server 2013 的部署方式

 

_**上次修改主題的時間：** 2012-10-03_

為 Lync 進行規劃時，首要決策在於如何部署 Microsoft Lync：做為內部部署的 Lync Server 2013 或是做為雲端中搭配 Microsoft Office 365 的 商務用 Skype Online。

  - 內部部署的 **Lync Server 2013：**此選擇可提供完整的 Lync 功能集，並在設定、自訂和操作部署作業時提供絕佳的彈性。所有伺服器皆安裝於現場，且由您的組織來維護。內部部署可提供完整的 Lync Server 功能。

  - 雲端中的 **商務用 Skype Online** 組織想要享受雲端立即訊息、目前狀態和會議的成本和靈活性效益，又不願犧牲 Lync Server 的企業等級功能， 商務用 Skype Online 就是專為這些組織而設計。藉由 商務用 Skype Online， Microsoft 可部署和維護必要的伺服器基礎結構，並處理持續不斷的維護、修補和升級作業。內部部署中部分可用功能無法在 商務用 Skype Online 中提供使用。

您最適合的部署類型取決於您想要部署的工作負載，及組織的地理位置和業務狀態。

## Lync Server

內部部署的 Lync Server 部署最適合下列案例：

  - **完整的 Enterprise Voice 功能** 如果您打算部署完整的 Enterprise Voice 方案，以取代 PBX 或使用進階通話功能的方案，需使用內部部署 Lync Server 部署。內部部署可支援使用 PBX 系統和主幹的直接連線，以及回應群組和通話駐留等進階電話功能。 Lync Online 目前不支援這些功能。

  - **媒體品質控制** 如果需要完整的媒體品質保證功能，例如通話許可控制服務 (CAC) 和服務品質 (QoS) 功能，您就需使用內部部署。

  - **常設聊天室** 如果您需為您的組織部署常設聊天室，您必須選擇內部部署。

  - **協力廠商伺服器應用程式** 僅內部部署才可使用信任的協力廠商應用程式，這些應用程式使用 Microsoft Unified Communications Managed API (UCMA)。

  - **需要地區性支援的跨國/跨地區公司** 如果您在多個國家或地區擁有資料中心，且需要依照地區來部署和管理伺服器，則內部部署最為適合，因為它可提供此類型的地區管理功能。

  - **對原則、報告和升級的完整控制權** 使用內部部署 Lync Server 部署時，您可擁有伺服器和用戶端原則、監控和其他報告，和升級時程等一系列的完整存取權。 Lync Online 可提供原則設定和報告的子集，並提供受限但重要的視窗以接受升級。

## Lync Online

如果對您而言，前述清單中沒有任何重要因素，則您可能會想要選擇 Lync Online 以擁有部署和管理上的簡易性。Lync Online 可提供健全的 IM、目前狀態和會議功能集，也可讓您組織的使用者透過 IP 互相進行語音和視訊通話。

