---
title: Lync Server 2013：在拓撲產生器中定義閘道
TOCTitle: 在拓撲產生器中定義閘道
ms:assetid: 456e5a96-d9f6-42a6-862c-a69464391628
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425945(v=OCS.15)
ms:contentKeyID: 49290774
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中於拓撲產生器內定義閘道

 

_**上次修改主題的時間：** 2012-10-04_

遵循本主題的步驟，使用 拓撲產生器來定義可以與 中繼伺服器建立關聯的 *對等* ，為啟用 企業語音的使用者提供公用交換電話網路 (PSTN) 的連線。 中繼伺服器的對等可以是您設定 SIP 主幹來連線的網際網路電話語音服務提供者 (ITSP) 的 PSTN 閘道、IP-PBX 或工作階段邊界控制器 (SBC)。

> [!NOTE]  
> 本主題假設您在至少一個具有組合或獨立 中繼伺服器的中央網站中已安裝至少一個內部 前端集區或 Standard Edition 伺服器，如部署移轉文件 <a href="lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md">在 Lync Server 2013 中定義和設定前端集區或 Standard Edition Server</a>和 <a href="lync-server-2013-publish-the-topology.md">在 Lync Server 2013 中發行拓撲</a>＞所述。本主題也假設您已確認基礎結構符合＜ <a href="lync-server-2013-software-prerequisites-for-enterprise-voice.md">Lync Server 2013 中 Enterprise Voice 的軟體先決條件</a>＞及＜ <a href="lync-server-2013-security-and-configuration-prerequisites-for-enterprise-voice.md">Lync Server 2013 中 Enterprise Voice 的安全性和組態先決條件</a>＞所述的先決條件。



## 定義中繼伺服器的對等

1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

2.  在 Lync Server 2013 下，在名稱為 Shared Components 的網站中，用滑鼠右鍵按一下 **\[PSTN 閘道\]** 節點，然後按一下 **\[新增 PSTN 閘道\]** 。
    
    ![拓撲產生器 Lync Server 2013](images/Gg425945.d898c3c1-8798-4b74-8f02-b994ef3db4c1(OCS.15).png "拓撲產生器 Lync Server 2013")

3.  在 **\[定義新的 IP/PSTN 閘道\]** 中，輸入對等的完整網域名稱 (FQDN) 或 IP 位址，然後按一下 **\[下一步\]** 。
    
    ![IP/PSTN 閘道](images/Gg425945.8017ba5e-41bc-48d4-97d9-fd306cd322b8(OCS.15).png "IP/PSTN 閘道")
    
    > [!NOTE]  
    > 如果您指定傳輸層安全性 (TLS) 作為傳輸類型，則必須指定 中繼伺服器對等的 FQDN，而非 IP 位址。
    


4.  定義您新的 PSTN 閘道的 IP 位址的聆聽模式 (IPv4 或 IPv6)，然後按一下 **\[下一步\]** 。
    
    ![IP 位址](images/Gg425945.c7fc0d12-adc8-45a7-aca1-b376e1d2fcec(OCS.15).png "IP 位址")

5.  定義 PSTN 閘道的 *根主幹* 。主幹是 中繼伺服器和 Tuple 唯一識別的閘道之間的邏輯連線。
    
    { 中繼伺服器 FQDN, 中繼伺服器聆聽連接埠 (TLS 或 TCP)：閘道 IP 與 FQDN、閘道聆聽連接埠}
    
      - 在 拓撲產生器中定義 PSTN 閘道時，您必須定義根主幹，才能將 PSTN 閘道成功新增至您的拓樸。
    
      - 必須先移除關聯的 PSTN 閘道，才能移除根主幹。
    
    ![定義閘道：根主幹](images/Gg425945.3b030757-eb35-4616-bb6b-74ee67507e3d(OCS.15).png "定義閘道：根主幹")

6.  在 **\[IP/PSTN 閘道的聆聽連接埠\]** 下，輸入聆聽連接埠，供閘道、PBX 或 SBC 用於聆聽來自將與 PSTN 閘道根主幹有關聯的 中繼伺服器的 SIP 訊息(依預設，在 PSTN 閘道、PBX 或 SBC 上，傳輸控制通訊協定 (TCP) 的連接埠為 5066，而傳輸層安全性 (TLS) 的連接埠為 5067。在分支網站的 Survivable Branch Appliance 上，TCP 的預設連接埠為 5081，而 TLS 的預設連接埠為 5082)。

7.  在 **\[SIP 傳輸通訊協定\]** 下，按一下對等使用的傳輸類型，然後按一下 **\[確定\]** 。
    
    > [!NOTE]  
    > 基於安全性理由，強烈建議您將對等部署至可使用 TLS 的 中繼伺服器。
    


8.  在 **\[關聯的 中繼伺服器\]** 下，選取 中繼伺服器集區，以建立與這個 PSTN 閘道的根主幹的關聯。

9.  在 **\[關聯的 中繼伺服器連接埠\]** 下，輸入 中繼伺服器的聆聽連接埠，以用來聆聽來自閘道的 SIP 訊息。
    
    > [!NOTE]  
    > 由於 Lync Server 2013 中支援多個主幹，因此可在 中繼伺服器上定義多個 SIP 訊號連接埠，用來與多個 PSTN 閘道進行通訊。定義主幹時， <strong>[關聯的 中繼伺服器連接埠]</strong> 必須在 中繼伺服器所允許的相關通訊協定的聆聽連接埠範圍之內。這個通訊埠範圍是根據 Lync Server 2013 和中繼集區來定義的。用滑鼠右鍵按一下需要的 中繼伺服器集區，然後選取 <strong>[編輯屬性]</strong> 。在 <strong>[聆聽連接埠]</strong> 欄位中指定連接埠範圍。
    


10. 按一下 \[完成\] 。

> [!IMPORTANT]  
> 繼續下一個步驟之前，請確定您定義的對等正在執行中，且使用您指定的 FQDN 或 IP 位址。



接下來，若要將對等新增至拓撲，請遵循部署文件 [在 Lync Server 2013 中發行拓撲](lync-server-2013-publish-the-topology.md)中的程序。每次使用 拓撲產生器建立或修改拓撲時，必須發行拓撲，以便使用資料安裝執行 Lync Server 的伺服器所需的檔案。

## 請參閱

#### 工作

[在 Lync Server 2013 的拓撲產生器中修改主幹](lync-server-2013-modify-a-trunk-in-topology-builder.md)

