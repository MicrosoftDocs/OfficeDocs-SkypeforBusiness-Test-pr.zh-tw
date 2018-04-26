---
title: Lync Server 2013：部署中繼伺服器並定義對等項目
TOCTitle: 部署中繼伺服器並定義對等項目
ms:assetid: a684f1da-6671-4011-adf6-2db49e2528e2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412780(v=OCS.15)
ms:contentKeyID: 49291906
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中部署中繼伺服器並定義對等項目

 

_**上次修改主題的時間：** 2012-09-21_

企業語音工作負載、電話撥入式會議和進階 企業語音應用程式 ( 回應群組應用程式、 通話駐留應用程式、通話許可控制 (CAC) 等) 均可用於 前端集區中。在 Lync Server 2013 中， 中繼伺服器功能已內建於 前端伺服器中。不再需要個別獨立的 中繼伺服器。 前端集區可與支援的閘道 (公用交換電話網路 (PSTN) 閘道或 IP-PBX) 直接通訊，就不需要以 中繼伺服器作為媒介。

唯一的例外狀況就是當您設定 SIP 主幹以連線到網際網路電話服務提供者的工作階段邊界控制器時。若要將 企業語音基礎結構連線到 SIP 主幹提供者，則必須部署個別的 中繼伺服器。

Lync Server ( 前端集區上的 中繼伺服器元件或獨立的 中繼伺服器) 與閘道之間的連線已定義成名為「主幹」 的邏輯關聯。本節中的主題說明如何定義主幹，以及如何在連線到 SIP 主幹的情況下，部署獨立的中繼伺服器。

## 本章節內容

  - [在 Lync Server 2013 的拓撲產生器中定義中繼伺服器](lync-server-2013-define-a-mediation-server-in-topology-builder.md)

  - [在 Lync Server 2013 中於拓撲產生器內定義閘道](lync-server-2013-define-a-gateway-in-topology-builder.md)

  - [在 Lync Server 2013 中安裝中繼伺服器的檔案](lync-server-2013-install-the-files-for-mediation-server.md)

  - [在 Lync Server 2013 中使用拓撲產生器定義其他主幹](lync-server-2013-define-additional-trunks-in-topology-builder.md)

## 相關各節

[在 Lync Server 2013 中設定撥入會議](lync-server-2013-configuring-dial-in-conferencing.md)

