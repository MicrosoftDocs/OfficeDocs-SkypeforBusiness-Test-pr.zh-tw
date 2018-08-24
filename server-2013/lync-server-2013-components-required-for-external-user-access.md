---
title: Lync Server 2013：外部使用者存取所需的元件
TOCTitle: 外部使用者存取所需的元件
ms:assetid: 2d0f9817-14e7-4109-95dc-62420e3c29e2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425779(v=OCS.15)
ms:contentKeyID: 49290452
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 外部使用者在 Lync Server 2013 中存取時所需的元件

 

_**上次修改主題的時間：** 2014-05-29_

大部分的 Edge 元件會部署在周邊網路上。周邊網路的 Edge 拓撲由下列元件組成。除非另有註明，這些元件均屬於 [Lync Server 2013 中的外部使用者存取案例](lync-server-2013-scenarios-for-external-user-access.md) 的一部分，且位於周邊網路中。Edge 元件包括：

  - Edge Server

  - 反向 Proxy

  - 防火牆

  - Director (選用，且是以邏輯方式位於周邊網路)

  - 調整式 Edge 拓撲的負載平衡 (DNS 負載平衡或硬體負載平衡器)
    
    > [!IMPORTANT]  
    > 不支援在一個介面上使用 DNS 負載平衡，而在另一個介面上使用硬體負載平衡。您必須同時針對這兩個介面使用硬體負載平衡或 DNS 負載平衡。
    


## Edge Server

Edge Server 可傳送及接收外部使用者對內部部署提供之服務的網路流量。 Edge Server 可執行下列服務：

  - **Access Edge Service**   Access Edge Service 能同時為輸出及輸入的工作階段初始通訊協定 (SIP) 流量提供單一、受信任的連線點。

  - **Web Conferencing Edge Service**   Web Conferencing Edge Service 可讓外部使用者參加您在內部 Lync Server 2013 部署上主辦的會議。

  - **A/V Edge Service**   A/V Edge Service 可讓外部使用者使用音訊、視訊、應用程式共用與檔案傳輸等功能。您的使用者可以在包含外部參與者的會議新增音訊和視訊，然後就可以在點對點工作階段中與外部使用者直接使用音訊及/或視訊進行通訊。A/V Edge Service 也可支援桌面共用與檔案傳輸。

  - **XMPP Proxy 服務**   XMPP Proxy 服務會接受來自設定之 XMPP 同盟協力廠商傳送的 XMPP (Extensible Messaging and Presence Protocol) 訊息，也會對其傳送 XMPP 訊息。

經授權的外部使用者可存取 Edge Server 以連線至您的內部 Lync Server 2013 部署，但 Edge Server 並不會提供任何其他內部網路存取。

> [!NOTE]  
> 部署 Edge Server 的目的是為啟用的 Lync 用戶端和其他 Microsoft Edge Server (在同盟案例中) 提供連線。設計的目的不是允許來自其他端點用戶端或伺服器類型的連線。可部署 XMPP 閘道伺服器，允許與設定的 XMPP 協力廠商進行連線。Edge Server 和 XMPP 閘道僅支援來自這些用戶端和同盟類型的端點連線。



## 反向 Proxy

下列作業需要反向 Proxy：

  - 讓使用者透過簡單 URL 連線至會議或電話撥入式會議

  - 讓外部使用者下載會議內容

  - 讓外部使用者能夠擴充通訊群組

  - 讓使用者取得可用於用戶端憑證式驗證的使用者式憑證

  - 讓遠端使用者從 Address Book Server 下載檔案，或送出查詢至通訊錄 Web 查詢服務

  - 讓遠端使用者取得用戶端與裝置軟體的更新

  - 使行動裝置能夠自動探索提供行動服務的 前端伺服器

  - 讓推入通知能夠從 Office 365 或 Apple 推入通知服務傳送到行動裝置

如需反向 Proxy 及其必須符合之要求的詳細資訊，請參閱＜ [Lync Server 2013 中的反向 Proxy 設定需求](lync-server-2013-configuration-requirements-for-reverse-proxy.md)＞中的詳細資訊。

> [!NOTE]  
> 外部使用者不需要透過虛擬私人網路 (VPN) 連線至您的組織才能使用 Lync Server 2013 參與通訊。若您已將 VPN 技術實作至組織中，且使用者為 Lync 使用了 VPN，就可能會對媒體流量 (例如視訊會議) 產生負面影響。您應考慮提供一種方法供媒體流量直接連線至 AV Edge 服務，並略過 VPN。如需詳細資訊，請參閱 NextHop 部落格文章＜啟用 Lync 媒體以略過 VPN 通道＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=256532" class="uri">http://go.microsoft.com/fwlink/?linkid=256532</a>。



## 防火牆

部署您的 Edge 拓撲時，您可以僅使用外部防火牆，也可以同時使用外部與內部防火牆。案例架構含有兩個防火牆。建議您使用兩個防火牆，因為這樣可確保從某個網路邊緣傳入另一個網路邊緣的流量嚴格遵守路由規則，且內部部署可受到兩層防火牆保護。

## Director

Director 是 Lync Server 2013 中選用的個別伺服器角色，不裝載使用者帳戶或提供目前狀態或會議服務。它會作為內部的「下一個躍點伺服器」，讓 Edge Server 將預定要進入內部伺服器的輸入 SIP 流量路由至該處。 Director 會預先驗證輸入要求，並將其重新導向至使用者的主集區或主伺服器。透過 Director 的預先驗證，您可從部署中未知的使用者帳戶移除要求。

Director 有助於 Enterprise Edition 前端集區中的 Standard Edition Server 與前端伺服器隔絕惡意流量，如拒絕服務 (DoS) 攻擊。如果網路上因此類攻擊而充斥無效的外部流量，這些流量將止於 Director。如需有關使用 Director 的詳細資訊，請參閱＜ [Lync Server 2013 中的 Director 案例](lync-server-2013-scenarios-for-the-director.md)＞。

## 請參閱

#### 概念

[Lync Server 2013 的硬體負載平衡器需求](lync-server-2013-hardware-load-balancer-requirements.md)

