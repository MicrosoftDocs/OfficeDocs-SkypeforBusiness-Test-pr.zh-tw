---
title: Lync Server 2013：中繼伺服器元件
TOCTitle: 中繼伺服器元件
ms:assetid: 5b19edef-4a54-43c9-aa12-5643b8108355
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398399(v=OCS.15)
ms:contentKeyID: 49291031
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的中繼伺服器元件

 

_**上次修改主題的時間：** 2012-09-21_

如果您部署 企業語音工作負載，必須一併部署 Lync Server 2013中繼伺服器。本節說明基本功能、相依性、基本拓撲以及規劃指南。

中繼伺服器可轉譯訊號，而且在某些組態中可轉譯內部 Lync Server 2013企業語音基礎結構及公用交換電話網路 (PSTN) 閘道或工作階段初始通訊協定 (SIP) 主幹之間的媒體。在 Lync Server 2013 端， 中繼伺服器會在單一相互 TLS (MTLS) 傳輸位址上聆聽。在閘道端，中繼伺服器會在所有與＜拓撲＞文件中所定義之主幹相關聯的相關聆聽連接埠上聆聽。所有合格的閘道都必須支援 TLS，不過也可以一併啟用 TCP。不支援 TLS 的閘道，仍舊可以支援 TCP。

如果您的環境中已經有一部公用交換機 (PBX)， 中繼伺服器會處理 企業語音使用者與 PBX 之間的所有通話。如果您的 PBX 是一部 IP-PBX，則您可以在 PBX 與 中繼伺服器之間建立直接的 SIP 連線。如果您的 PBX 是一部分時多工 (TDM) PBX，則您必須同時在 中繼伺服器與 PBX 之間部署一個 PSTN 閘道。

中繼伺服器預設會與 前端伺服器組合在一起。 中繼伺服器也可以部署在獨立的集區中以提高效能，如果您部署了 SIP 主幹，則強烈建議您在獨立的集區中進行部署。

如果您對支援媒體旁路和 DNS 負載平衡的合格 PSTN 閘道部署了直接 SIP 連線，就不需要獨立的中繼伺服器集區。因為合格閘道能夠將 DNS 負載平衡分攤到中繼伺服器集區，讓後者接收集區中其他 中繼伺服器的流量，所以就不需要獨立的 中繼伺服器集區。

當您部署 IP-PBX 或連線至網際網路電話語音伺服器提供者的工作階段邊界控制器 (SBC) 時，只要符合下列任何條件，我們也會建議您在 前端集區上組合 中繼伺服器：

  - IP-PBX 或 SBC 設定為接收集區中任何 中繼伺服器的流量，並一律將流量傳送至集區中的所有 中繼伺服器。

  - IP-PBX 不支援媒體旁路，但是主控 中繼伺服器的 前端集區可以針對不適用媒體旁路的呼叫進行語音轉碼處理。

您可以使用 Microsoft Lync Server 2013 規劃工具評估將 中繼伺服器組合於某個 前端集區時，前端集區是否可處理這些負載。如果環境無法符合這些需求，則您必須部署獨立的 中繼伺服器集區。

中繼伺服器的主要功能如下：

  - 在 Lync Server 端加密與解密 SRTP

  - 將透過 TCP 的 SIP (對於不支援 TLS 的閘道) 轉譯為透過相互 TLS 的 SIP

  - 轉譯 Lync Server 與 中繼伺服器閘道對等實體之間的媒體資料流

  - 將網路外部的用戶端連線到內部 ICE 元件，這些元件可以讓媒體周遊 NAT 與防火牆

  - 做為閘道不支援之通話流程的中介者，例如來自 企業語音用戶端上的遠端工作者的通話

  - 在包含 SIP 主幹的部署中，搭配使用 SIP 主幹服務提供者可提供 PSTN 支援，如此便不需要 PSTN 閘道

下圖顯示 中繼伺服器與基本 PSTN 閘道及 企業語音基礎結構通訊時使用的訊號和媒體通訊協定。

**中繼伺服器使用的訊號和媒體通訊協定**

![中繼伺服器通訊協定圖表](images/Gg398399.c3d39ba0-e323-4a58-8f07-4e80d3278af2(OCS.15).jpg "中繼伺服器通訊協定圖表")

> [!NOTE]  
> 如果您在 PSTN 閘道與 中繼伺服器之間的網路上使用 TCP 或 RTP/RTCP (而非 SRTP 或 SRTCP)，建議您採取相關措施以協助確保網路的安全性及隱私。



## 本節內容

  - [Lync Server 2013 中的 M:N 主幹](lync-server-2013-m-n-trunk.md)

  - [Lync Server 2013 中的通話許可控制和中繼伺服器](lync-server-2013-call-admission-control-and-mediation-server.md)

  - [Lync Server 2013 中的增強型 9-1-1 (E9-1-1) 和中繼伺服器](lync-server-2013-enhanced-9-1-1-e9-1-1-and-mediation-server.md)

  - [Lync Server 2013 中的媒體旁路和中繼伺服器](lync-server-2013-media-bypass-and-mediation-server.md)

  - [Lync Server 2013 中之中繼伺服器的元件和拓撲](lync-server-2013-components-and-topologies-for-mediation-server.md)

  - [Lync Server 2013 中的中繼伺服器的部署指導方針](lync-server-2013-deployment-guidelines-for-mediation-server.md)

