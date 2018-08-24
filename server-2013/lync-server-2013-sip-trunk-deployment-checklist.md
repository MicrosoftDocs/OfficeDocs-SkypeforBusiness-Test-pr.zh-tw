---
title: Lync Server 2013：SIP 主幹部署檢查表
TOCTitle: SIP 主幹部署檢查表
ms:assetid: 94f4f03e-19d5-4198-92be-e4076dbb959a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398755(v=OCS.15)
ms:contentKeyID: 49291697
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的 SIP 主幹部署檢查表

 

_**上次修改主題的時間：** 2012-09-21_

在部署 SIP 主幹之前，您和服務提供者必須交換和雙方 SIP 主幹端點相關的某些基本連線資訊。

請針對每個要連接的 ITSP 閘道取得下列資訊：

  - IP 位址

  - 網域全名 (FQDN)

> [!NOTE]  
> 服務提供者可能會要求您連接多個 ITSP 閘道。在這種情況下，您必須在每個 ITSP 閘道和集區中的每部 中繼伺服器之間設定連線。



提供給服務提供者的資訊取決於您的 SIP 主幹連線類型：

  - 對於多重通訊協定標籤交換 (Multiprotocol Label Switching，MPLS) 或私人網路連線，請將周邊網路 (亦稱為 DMZ、非軍事區及遮蔽式子網路) 中路由器的可公開路由傳送 IP 位址提供給 ITSP。確認 ITSP 的閘道或工作階段界限控制器 (SBC) 可連接此位址。另請將 中繼伺服器的 FQDN 提供給 ITSP。

  - 對於虛擬私人網路 (VPN) 連線，請將 VPN 伺服器的 IP 位址提供給 ITSP。

## 憑證考量

若要判斷您是否需要 SIP 主幹的憑證，請洽詢 ITSP 有關通訊協定支援的事宜：

1.  如果 ITSP 僅支援傳輸控制通訊協定 (TCP)，您便不需要憑證。

2.  如果 ITSP 支援傳輸層安全性 (TLS)，則 ITSP 必須提供憑證給您。

> [!NOTE]  
> SIP 能和即時傳輸通訊協定 (RTP) 或安全即時傳輸通訊協定 (SRTP) 搭配運作，其為管理 Voice over Internet Protocol (VoIP) 通話中實際語音資料的通訊協定。



## 部署程序

若要實作 SIP 主幹連線的 Lync Server 側，請遵循下列步驟：

1.  使用 Lync Server  拓撲產生器來建立和設定 SIP 網域拓撲。如需詳細資訊，請參閱部署文件中的 [針對 Lync Server 2013 在拓撲建置器中定義和設定拓撲](lync-server-2013-define-and-configure-a-topology-in-topology-builder.md)。

2.  使用 Lync Server 控制台來設定新 SIP 網域的語音路由。如需詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中設定主幹](lync-server-2013-configuring-trunks.md)。

3.  使用 **Test-CsPstnOutboundCall** Cmdlet 來測試連線。如需詳細資訊，請參閱 Lync Server 管理命令介面文件或 Lync Server 管理命令介面的說明。

