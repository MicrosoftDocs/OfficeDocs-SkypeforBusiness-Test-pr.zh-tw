---
title: 網路基礎結構需求
TOCTitle: 網路基礎結構需求
ms:assetid: 35c7bb3f-8e0f-48b7-8a2c-857d4b42a4c4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425841(v=OCS.15)
ms:contentKeyID: 49290563
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 網路基礎結構需求

 

_**上次修改主題的時間：** 2014-08-28_

Lync Server 2013 拓撲中各伺服器的網路介面卡都必須支援每秒至少 1 Gbps。一般而言，您應該使用低延遲和高頻寬的區域網路 (LAN) 來連線 Lync Server 拓撲內所有的伺服器角色。LAN 的大小視拓撲的大小而定：

  - 在 Standard Edition 拓撲中，伺服器應位於支援 1 Gbps 乙太網路或相等的網路中。

  - 在前端集區拓撲中，大部分的伺服器應位於支援 1 Gbps 以上的網路中，特別是在支援視訊/音訊 (A/V) 會議和應用程式共用時。

針對公用交換電話網路 (PSTN) 整合，您可以使用 T1/E1 線路或 SIP 主幹來整合。

## 視訊/音訊網路需求

在 Lync Server 部署中，視訊/音訊 (A/V) 的網路需求如下所示：

  - 如果您正在使用 DNS 負載平衡來部署單一 Edge Server 或 Edge 集區，可以設定外部防火牆以作為 NAT。內部防火牆不可設定為 NAT。如需這些需求的詳細資訊，請參閱規劃文件中的＜[決定 Lync Server 2013 的外部 A/V 防火牆和連接埠需求](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md)＞。
    
    > [!IMPORTANT]  
    > 如果您有 Edge 集區且正在使用硬體負載平衡器，您必須在每個 Edge Server 上使用公用 IP 位址，而且不能針對 NAT 裝置上的伺服器或集區使用 NAT (例如，防火牆，或者會有 NAT 輸入或輸出流量的其他基礎結構裝置)。如需詳細資訊，請參閱＜外部使用者存取規劃＞文件中的＜<a href="lync-server-2013-port-summary-scaled-consolidated-edge-with-hardware-load-balancers.md">Lync Server 2013 中的連接埠摘要 - 調整式合併 Edge (利用硬體負載平衡器)</a>＞。
    


  - 如果您的組織使用的是服務品質 (QoS) 基礎結構，則媒體子系統將會設計成配合此現有基礎結構運作。

  - 如果您使用網際網路通訊協定安全性 (IPsec)，建議您針對 A/V 流量所使用的連接埠範圍停用 IPsec。如需詳細資訊，請參閱規劃文件中的＜[Lync Server 2013 中的 IPsec 例外](lync-server-2013-ipsec-exceptions.md)＞。

為了確保最佳的媒體品質，請執行下列作業：

  - 佈建您的網路連結，以支援每個音訊資料流具備 65 Kbps 的傳輸量與每個視訊資料流具備 500 Kbps 的傳輸量 (啟用時在尖峰時段的速率)。雙向音訊或視訊工作階段包含兩種資料流。

  - 為了因應高於此等級的突發性流量暴增與使用一段時間之後的流量增加，Lync Server 媒體端點可以依據各種網路條件進行調整並在維持可接受的品質前提下，支援三倍的音訊與視訊傳輸量負載 (請參閱先前的段落說明)。但是，請勿認為這項調整功能可以支援未佈建齊全的網路。在未佈建齊全的網路中，Lync Server 媒體端點動態處理各種網路狀況的能力 (例如暫時性的大量封包遺失情況) 會降低。

  - 對於佈建成本與困難度非常高的網路連結來說，您可能不得不考慮以較低的流量為主進行佈建。在此情況中，請讓 Lync Server 媒體端點的彈性吸收流量與尖峰流量等級之間的差距，這當中可能會損失一些語音品質。同時，也會減少用來吸收突發性流量暴增的空間。

  - 對於無法在短時間內正確佈建的連結來說 (例如 WAN 連結品質非常差的網站)，請考慮針對某些使用者停用視訊功能。

  - 佈建網路時，請確保在尖峰用量時段保持最高 150 ms 的端對端延遲水準。延遲情況是 Lync Server 媒體元件無法排除的網路障礙之一，因此如何找到與消除此弱點變成了重要課題。

  - 對於執行防毒軟體的伺服器，請將所有執行 Lync Server 的伺服器都納入例外清單中，以達到最佳效能和音訊品質。

## 會議網路需求

用於從 Internet Information Services (IIS) 伺服器下載會議內容的頻寬需視上傳的內容大小而定。

