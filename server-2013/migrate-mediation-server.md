---
title: 移轉中繼伺服器
TOCTitle: 移轉中繼伺服器
ms:assetid: b0b77121-2c8f-413e-b276-dbf1038361d3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205173(v=OCS.15)
ms:contentKeyID: 49292023
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉中繼伺服器

 

_**上次修改主題的時間：** 2012-09-28_

當您執行 \[合併精靈\] 時，中繼伺服器會合併到您 Lync Server 2013 的試驗拓撲中。由於 Office Communications Server 2007 R2 集區無法與 Lync Server 2013 中繼伺服器通訊，因此您必須等待所有使用者完成移轉之後，再設定 Lync Server 2013 中繼伺服器。 Lync Server 2013 集區會在進行並存移轉時，與 Office Communications Server 2007 R2 中繼伺服器通訊。

當您設定 Lync Server 2013 中繼伺服器時，還必須升級或置換您的 Office Communications Server 2007 R2 閘道。 Office Communications Server 2007 R2 閘道不支援 Lync Server 2013 中繼伺服器。您必須部署 Lync Server 2013 認可的閘道，並將他們關聯至 Lync Server 2013 中繼伺服器。您必須執行此步驟，才可完全解除委任 Office Communications Server 2007 R2 部署。

本節中的各主題說明在完成移轉 Lync Server 2013 中繼伺服器之後需要執行的設定工作。將組合的中繼伺服器轉換為獨立的中繼伺服器是選用工作。

  - [設定中繼伺服器](configure-mediation-server.md)

  - [變更語音路由以使用新的 Lync Server 2013 中繼伺服器](change-voice-routes-to-use-the-new-lync-server-2013-mediation-server.md)

  - [將組合的中繼伺服器轉換成獨立中繼伺服器 (選用)](transition-a-collocated-mediation-server-to-a-stand-alone-mediation-server-optional.md)

