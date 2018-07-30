---
title: Lync Server 2013：PSTN 連線元件
TOCTitle: PSTN 連線元件
ms:assetid: 6b2a3f7d-760f-4f09-8432-312c98a7e6b7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398504(v=OCS.15)
ms:contentKeyID: 49291220
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 PSTN 連線元件

 

_**上次修改主題的時間：** 2012-10-04_

企業等級的 VoIP 解決方案必須提供與公用交換電話網路 (PSTN) 之間的往來通話，且不犧牲任何服務品質 (QoS)。此外，使用者在撥號及接聽電話時應該不會意識到此基礎技術的存在。就使用者的觀點而言，Enterprise Voice 基礎結構與 PSTN 之間的通話應該就像是另一個 SIP 工作階段。

針對 PSTN 連線，您可以部署 SIP 主幹或 PSTN 閘道 (含有 PBX (也稱為直接 SIP 連結) 或沒有 PBX)。

## SIP 主幹

若不使用 PSTN 閘道，替代的方法是使用 SIP 主幹將 Enterprise Voice 方案連線至 PSTN。SIP 主幹可啟用下列案例：

  - 公司防火牆內外的企業使用者可透過符合 E.164 格式號碼所指定，且以 PSTN (做為對應服務提供者之服務) 為電話終端，來撥打市內或長途電話。

  - 任何 PSTN 訂閱者都可以透過撥打與企業使用者相關聯的直接向內撥號 (DID) 號碼，與位於公司防火牆內外的企業使用者連絡。

使用這個部署解決方案必須有 SIP 主幹服務提供者。

## PSTN 閘道

PSTN 閘道是協力廠商裝置，可轉譯 Enterprise Voice 基礎結構與 PSTN 或 PBX 之間的訊號和媒體。PSTN 閘道與中繼伺服器搭配運作，以向 Enterprise Voice 用戶端呈現 PSTN 或 PBX 通話。中繼伺服器也會向 PSTN 閘道呈現來自 Enterprise Voice 用戶端的通話，以路由傳送至 PSTN 或 PBX。如需與 Microsoft 合作提供使用 Lync Server 之裝置的協力廠商清單，請參閱 Microsoft Unified Communications Partners 網站，網址為 [http://go.microsoft.com/fwlink/?linkid=202836\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=202836%26clcid=0x404)。

## 專用交換機

如果您的現有語音基礎結構使用專用交換機 (PBX)，則可以搭配使用 PBX 與 Lync Server Enterprise Voice。

支援的 Enterprise Voice PBX 整合案例如下：

  - 支援媒體旁路且含有中繼伺服器的 IP-PBX。

  - 需要獨立 PSTN 閘道的 IP-PBX。

  - 含有獨立 PSTN 閘道的分時多工 (TDM) PBX。

> [!NOTE]  
> 媒體旁路不會與每個 PSTN 閘道、IP-PBX 以及 SBC 相互溝通。Microsoft 已經與認證的合作夥伴測試了一組 PSTN 閘道和 SBC，並用 Cisco IP-PBX 完成部分測試。只有列在 Unified Communications Open Interoperability Program – Lync Server 中的產品和版本支援媒體旁路，網址為：<a href="http://go.microsoft.com/fwlink/p/?linkid=214406">http://go.microsoft.com/fwlink/p/?linkId=214406</a>。



如需提供 Enterprise Voice 方案之協力廠商的詳細資訊，請參閱 Microsoft Unified Communications Partners 網站，網址為 [http://go.microsoft.com/fwlink/?linkid=202836\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=202836%26clcid=0x404)。

如需提供 Enterprise Voice 硬體解決方案 (包括 PSTN 閘道) 之協力廠商的詳細資訊，請參閱 Microsoft Unified Communications Partners 網站，網址為 [http://go.microsoft.com/fwlink/?linkid=202836\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=202836%26clcid=0x404)。

