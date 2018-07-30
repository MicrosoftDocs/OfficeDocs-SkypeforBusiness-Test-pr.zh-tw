---
title: Lync Server 2013 裝置硬體支援
TOCTitle: 裝置硬體支援
ms:assetid: ba07ca91-32b4-49cf-801c-47a2d1d96e18
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412908(v=OCS.15)
ms:contentKeyID: 49292137
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的裝置硬體支援

 

_**上次修改主題的時間：** 2012-12-14_

特定硬體設定必須已就緒，才能部署 IP 電話和類比裝置。

執行 Lync Phone Edition的 IP 電話支援 Link Layer Discovery Protocol-Media Endpoint Discovery (LLDP-MED) 和 Power over Ethernet (PoE)。若要利用 LLDP-MED，交換器必須支援 IEEE802.1AB 和 ANSI/TIA-1057。若要利用 PoE，交換器必須支援 PoE802.3AF 或 802.3at。

若要啟用 LLDP-MED，管理員必須透過使用交換器主控台視窗來啟用 LLDP，然後使用正確的語音 VLAN ID 來設定 LLDP-MED 網路原則。

另外，如果您的部署包含類比裝置，則必須設定類比閘道使用 Lync Server，且該閘道必須是下列其中一種：

  - 類比電話配接器 (ATA)

  - PSTN 類比閘道

  - 內含 PSTN 類比閘道的基本分公司設備

  - 內含可以 ATA 通訊之 PSTN 閘道的基本分公司設備

若要了解如何設定類比閘道，請參閱 Lync Server 2010 TechNet Library 中的＜規劃部署類比裝置＞(可能為英文網頁)，網址為： [http://go.microsoft.com/fwlink/?linkid=268537\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268537%26clcid=0x404)。(類比裝置在 Lync Server 2013 的運作方式與 Lync Server 2010 相同。)

> [!IMPORTANT]  
> 您可以將交換器設定為支援增強型 9-1-1 (E9-1-1) (如果交換器支援此設定)。


