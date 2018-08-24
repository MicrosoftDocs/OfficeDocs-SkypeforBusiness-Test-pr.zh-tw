---
title: Lync Server 2013：SIP 主幹連線的元件與拓撲
TOCTitle: SIP 主幹連線的元件與拓撲
ms:assetid: 8ed9a9d0-517e-4f36-a131-22cdafa257fa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398720(v=OCS.15)
ms:contentKeyID: 49291637
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 SIP 主幹連線的元件與拓撲

 

_**上次修改主題的時間：** 2012-09-21_

下圖說明 Lync Server 中的 SIP 主幹拓撲。

**SIP 主幹拓撲**

![SIP 主幹拓撲](images/Gg398720.669fb55d-7c81-4e21-9421-fabc43d6e064(OCS.15).jpg "SIP 主幹拓撲")

如圖所示，企業網路和公用交換電話網路 (PSTN) 服務提供者之間是使用 IP 虛擬私人網路 (VPN) 進行連線。這個私人網路的作用在於提供 IP 連線、提升安全性，以及 (選用) 取得服務品質 (QoS) 保證。由於 VPN 的性質所致，您不需要將傳輸層安全性 (TLS) 用於 SIP 訊號流量，或是將安全即時傳輸通訊協定 (SRTP) 用於媒體流量。因此企業和服務提供者之間的連線是由一般 TCP 連線和一般即時傳輸通訊協定 (RTP) (透過 UDP) 所組成，前者用於 SIP 作業，後者用於傳送透過 IP VPN 穿隧而來的媒體。請確定 VPN 路由器之間的所有防火牆都已開啟連接埠，以允許 VPN 路由器進行通訊，而且 VPN 路由器外部邊緣上的 IP 位址可公開進行路由傳送。

> [!IMPORTANT]
> 請連絡服務提供者以判斷其是否可提供高可用性支援 (包括容錯移轉)。如果可以，您便需要判斷設定的程序。例如，是否只需要在每部 中繼伺服器上設定一個 IP 位址和一個 SIP 主幹，還是需要在每部 中繼伺服器上設定多個 SIP 主幹？<br />
> 如果您有多個 中央網站，另請詢問服務提供者是否有能力啟用與另一個 中央網站間的雙向連線。


> [!NOTE]  
> 對於 SIP 主幹，我們強烈建議您部署獨立 中繼伺服器。如需詳細資訊，請參閱部署文件中的 <a href="lync-server-2013-deploying-mediation-servers-and-defining-peers.md">在 Lync Server 2013 中部署中繼伺服器並定義對等項目</a>。



## 保護用於 SIP 主幹的中繼伺服器

基於安全因素，您應該為兩個 VPN 路由器間的各個連線設定虛擬 LAN (VLAN)。設定 VLAN 的實際程序會由於路由器製造商不同而有所差異。如需詳細資訊，請連絡路由器製造商。

我們建議您遵循以下指導方針：

  - 在周邊網路 (亦稱為 DMZ、非軍事區及遮蔽式子網路) 的 中繼伺服器和 VPN 路由器之間設定虛擬 LAN (VLAN)。

  - 請勿允許從路由器將廣播或多點傳送封包傳輸至 VLAN。

  - 封鎖任何從路由器將流量路由傳送至 中繼伺服器以外任何位置的路由規則。

如果您使用 VPN 伺服器，我們建議您遵循以下指導方針：

  - 在 VPN 伺服器和 中繼伺服器之間設定 VLAN。

  - 請勿允許從 VPN 伺服器將廣播或多點傳送封包傳輸至 VLAN。

  - 封鎖任何將 VPN 伺服器流量路由傳送至 中繼伺服器以外任何位置的路由規則。

  - 使用 Generic Routing Encapsulation (GRE) 加密 VPN 上的資料。

