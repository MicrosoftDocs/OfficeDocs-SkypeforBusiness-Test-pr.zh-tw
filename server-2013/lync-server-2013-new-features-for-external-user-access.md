---
title: Lync Server 2013：外部使用者存取的新功能
TOCTitle: 外部使用者存取的新功能
ms:assetid: 99da6bd5-ec14-4ad9-8f7d-37fbddf567dd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398794(v=OCS.15)
ms:contentKeyID: 49291762
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中外部使用者存取的新功能

 

_**上次修改主題的時間：** 2012-10-17_

Lync Server 2013 引進新的功能，為使用者擴充各項功能及通訊方法。 Lync Server 2013 同時也引進對現有服務的變更，讓組織可用的服務獲得更好的整合與延伸。對於可能影響您規劃及部署 Lync Server 2013  Edge Server 服務時的變更，提供摘要如下。

  - **支援 IPv6 定址**     Lync Server 2013 可對所有 Edge Server 服務支援 IPv6 定址。如果您已透過 Windows Server 中的組態為介面提供 IPv6 位址，即可透過 拓撲產生器中的 IP 位址組態，在 Edge Server 組態中使用 IPv6 位址。
    
    > [!IMPORTANT]  
    > 若要在 Lync Server 2013 中使用 IPv6 位址，貴組織部署的路由器和防火牆中必須支援 IPv6，且網際網路服務提供者也必須提供 IPv6 支援。
    


  - **可延伸傳訊和顯示狀態通訊協定 (XMPP)**     Lync Server 2013 中引進完全整合的 XMPP Proxy (部署於 Edge Server) 和 XMPP 閘道 (部署於 前端伺服器)。您還可以選擇是否部署 XMPP 同盟這個選用元件。新增並設定 XMPP Proxy 和 XMPP 閘道可以讓您的 Microsoft Lync 2013 使用者從 XMPP 型合作夥伴那裡新增立即訊息 (IM) 與目前狀態所用的連絡人。
    
    > [!NOTE]  
    > 目前 Lync Server 2013 中的 XMPP 服務僅在 Lync 用戶端與 XMPP 型連絡人之間提供立即訊息與目前狀態服務。
    


  - **行動用戶端的行動服務**     Lync Server 2013 中的行動服務最初是在 Lync Server 2010 的客戶更新中引進，可讓行動電話或平板電腦裝置 (需使用受支援的 Apple iOS、Android、Windows Phone 或 Nokia 行動裝置) 上的 Microsoft Lync Mobile 用戶端執行如傳送與接收立即訊息、檢視連絡人及檢視目前狀態等活動。此外，行動裝置還可支援某些 Enterprise Voice 功能，例如按一下加入會議、從公司撥號、單一號碼搜尋、語音信箱及未接來電通知。
    
    > [!NOTE]  
    > 行動服務會使用您 前端伺服器上部署的反向 Proxy 與已發行的服務。不需要對 Edge Server 進行任何變更。
    


  - **Director 是選用角色**     Director 伺服器在 Lync Server 2013 拓撲中的角色不變。它仍然裝載 Web 服務、預先驗證傳入的使用者要求，並將外部使用者導向適當的主集區。將 Director 從建議的角色變更為選用角色並不會削減 Director 的價值，而是能夠減少伺服器數量和其他硬體需求 (例如， Director 的硬體負載平衡器) ，又不會讓功能受到危害。由於 前端伺服器可以執行與 Director 相同的工作，而不會對已提供的服務有任何影響，因此您可以選擇是否要部署 Director。您可以放心地排除 Director，確信 前端伺服器將能夠代替其提供相同的服務。

## 請參閱

#### 概念

[在 Lync Server 2013 中規劃和設定 IPv6](lync-server-2013-planning-for-and-configuring-ipv6.md)  

#### 其他資源

[在 Lync Server 2013 中規劃外部使用者存取](lync-server-2013-planning-for-external-user-access.md)  
[規劃 Lync Server 2013 中的可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟](lync-server-2013-planning-for-extensible-messaging-and-presence-protocol-xmpp-federation.md)

