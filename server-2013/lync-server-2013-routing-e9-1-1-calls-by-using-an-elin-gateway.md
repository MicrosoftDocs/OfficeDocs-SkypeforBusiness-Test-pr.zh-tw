---
title: Lync Server 2013：使用 ELIN 閘道路由 E9-1-1 來電
TOCTitle: 使用 ELIN 閘道路由 E9-1-1 來電
ms:assetid: 5a3997e3-898d-49cb-922a-4184c3373350
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204919(v=OCS.15)
ms:contentKeyID: 49291017
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中使用 ELIN 閘道路由 E9-1-1 來電

 

_**上次修改主題的時間：** 2013-02-05_

Unified Communications Open Interoperability Program 中的部分協力廠商提供具備合格緊急位置識別號碼 (ELIN) 功能的閘道，此類閘道可以用來做為與合格 E9-1-1 服務提供者的 SIP 主幹連線替代項目。ELIN 閘道支援ISDN 或與以公用交換電話網路 (PSTN) 為基礎之 E9-1-1 服務的集中式自動通話記帳系統 (CAMA) 連線。如需有關提供 ELIN 閘道之協力廠商及其文件連結的詳細資訊，請參閱 <http://go.microsoft.com/fwlink/?linkid=248425>。

就像與 E9-1-1 服務提供者的 SIP 主幹連線，ELIN 閘道也會提供將緊急通話路由傳送至最適合來電者的公共安全勤務中心 (PSAP) 的工具，但這些閘道會使用 ELIN 做為位置識別碼。您會針對組織中的每個緊急回應位置 (ERL) 定義 ELIN (如需詳細資訊，請參閱＜ [在 Lync Server 2013 中管理 ELIN 閘道的位置](lync-server-2013-managing-locations-for-elin-gateways.md)＞)。

當您針對緊急通話使用 ELIN 閘道時，會使用與您針對 SIP 主幹連線使用的相同 Lync Server E9-1-1 基礎結構。也就是， 位置資訊服務資料庫會為 Lync Server 用戶端提供位置，而且位置原則會啟用此功能並定義路由。但是，使用 ELIN 閘道時，您必須將 ELIN 新增至 位置資訊服務資料庫，而且要透過 PSTN 電訊廠商將它們上載至自動位置識別 (ALI) 資料庫。

當 Lync 用戶端從 位置資訊服務取得它的位置時，位置會包含 ELIN。在緊急通話期間，ELIN 會包含於傳送至 ELIN 閘道的位置中。ELIN 閘道會將該通話識別為緊急通話，並使用 ELIN 來交換來電者的號碼。ELIN 閘道接著會將通話路由傳送至含有 ELIN 的 PSTN 做為來電號碼。PSTN E9-1-1 提供者會在 ALI 資料庫中查閱該 ELIN，此為主要街道地址指南 (MSAG) 資料庫隨附的資料庫。PSTN 接著會根據 ALI 查閱，將通話傳送到最適當的 PSAP，而 PSAP 會根據 ALI 查閱，將第一位回應者傳送至來電者的位置。系統會將來電號碼快取於 ELIN 閘道上一段預設的時間以利回撥。PSAP 會在回撥期間到達 ELIN 閘道，其會針對來電者的直接向內撥號 (DID) 號碼交換 ELIN。

ELIN 閘道僅支援來自組織網路內的緊急通話。它們不支援從您網路外部撥打的緊急通話。

> [!NOTE]  
> 如需有關針對緊急通話使用 SIP 主幹連線的詳細資訊，請參閱＜ <a href="lync-server-2013-routing-e9-1-1-calls-by-using-a-sip-trunk.md">在 Lync Server 2013 中使用 SIP 主幹路由 E9-1-1 來電</a>＞。



下圖顯示當您使用 ELIN 閘道時，如何將緊急通話從 Lync Server 路由傳送至 PSAP。

**利用 ELIN 閘道路由傳送 E9-1-1 通話**

![ELIN 電話路由](images/JJ204919.ea68f88a-0fc4-43d4-9660-79a7e8936df1(OCS.15).jpg "ELIN 電話路由")

1.  包含位置、來電者的回撥號碼及 (選用) 通知 URL 和會議回撥號碼的 SIP INVITE 會路由傳送至 Lync Server。

2.  Lync Server 會比對緊急號碼，然後將通話 (根據適當位置原則中定義的 \[PSTN 使用方式\] 值) 路由傳送至 中繼伺服器，然後從該處路由傳送至 ELIN 閘道。

3.  ELIN 閘道會透過 ISDN 或 CAMA 主幹，將通話路由傳送至 PSTN。

4.  PSTN 會將該通話識別為緊急通話，並將它路由傳送至網路中 E9-1-1 選擇的路由器。E9-1-1 選擇的路由器會在 ALI 資料庫中查閱來電者的號碼，以取得地理位置。E9-1-1 選擇的路由器會根據從 ALI 資料庫擷取的位置資訊，將通話路由傳送至最適當的 PSAP。

5.  如果您已設定通知的位置原則，就會將特殊的 Lync 緊急通知立即訊息傳送給組織的一或多個安全人員。此訊息一律會快顯在安全人員的螢幕上，並包含發話者的名稱、電話號碼、時間和位置，讓安全人員能夠使用立即訊息或語音，快速回應緊急發話者。

6.  如果通話提前中斷，PSAP 會使用 ELIN，直接與來電者連絡。ELIN 閘道會針對來電者的 DID 交換 ELIN。

