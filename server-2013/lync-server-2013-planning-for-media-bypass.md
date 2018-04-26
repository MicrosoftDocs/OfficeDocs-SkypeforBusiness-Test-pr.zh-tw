---
title: Lync Server 2013：規劃媒體旁路
TOCTitle: 規劃媒體旁路
ms:assetid: 8ac732b6-8538-4d7b-b1a9-2035e419dac2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398703(v=OCS.15)
ms:contentKeyID: 49291593
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中規劃媒體旁路

 

_**上次修改主題的時間：** 2012-09-21_

媒體旁路表示盡可能為訊號周遊在中繼伺服器中的通話移除媒體路徑上的中繼伺服器。

媒體旁路能減少延遲時間、不必要的轉譯、封包遺失率及可能的失敗點數，進而提升語音品質。由於經過旁路處理的通話能省去媒體處理的需求，減輕中繼伺服器的負載，因此能提升延展性。減輕的負載能補足 中繼伺服器控制多個閘道的能力。

當不具有 中繼伺服器的分支網站透過一個或多個啟用頻寬限制的 WAN 連結與中央網站連接時，媒體旁路能讓分支網站之用戶端的媒體直接流向本地閘道，而不需要先經由 WAN 連結流向中央網站的 中繼伺服器後再返回，藉此降低頻寬需求。

藉由減輕 中繼伺服器的媒體處理負擔，媒體旁路還能減少 企業語音基礎結構所需的 中繼伺服器數量。

下圖表示啟用媒體旁路和未啟用媒體旁路之拓撲中的基本媒體和訊號路徑。

**啟用媒體旁路和未啟用媒體旁路時的媒體和訊號路徑**

![強制語音 CAC 媒體旁路連線](images/Gg398703.4d66d529-0912-4de1-abec-266f54272eb3(OCS.15).jpg "強制語音 CAC 媒體旁路連線")

依照通則，請盡可能啟用媒體旁路。

## 本章節內容

  - [Lync Server 2013 中的媒體旁路概觀](lync-server-2013-overview-of-media-bypass.md)

  - [Lync Server 2013 中的媒體旁路模式](lync-server-2013-media-bypass-modes.md)

  - [Lync Server 2013 中的媒體旁路和通話許可控制](lync-server-2013-media-bypass-and-call-admission-control.md)

  - [Lync Server 2013 中媒體旁路的技術需求](lync-server-2013-technical-requirements-for-media-bypass.md)

## 相關各節

[在 Lync Server 2013 中部署進階 Enterprise Voice 功能](lync-server-2013-deploying-advanced-enterprise-voice-features.md)

## 請參閱

#### 工作

[在 Lync Server 2013 中設定含媒體旁路的主幹](lync-server-2013-configure-a-trunk-with-media-bypass.md)  

#### 概念

[Lync Server 2013 中的全域媒體旁路選項](lync-server-2013-global-media-bypass-options.md)

