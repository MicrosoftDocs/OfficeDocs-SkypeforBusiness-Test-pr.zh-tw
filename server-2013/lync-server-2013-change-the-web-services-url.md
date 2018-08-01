---
title: 在 Lync Server 2013 中變更 Web 服務 URL
TOCTitle: 在 Lync Server 2013 中變更 Web 服務 URL
ms:assetid: 4cee37c0-3b99-4207-997f-bf4229d760c0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520992(v=OCS.15)
ms:contentKeyID: 49290851
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中變更 Web 服務 URL

 

_**上次修改主題的時間：** 2014-02-07_

當您設定前端集區和 Standard Edition Server 時，可以選擇設定外部 Web 伺服器陣列完整網域名稱 (FQDN) 和相關聯的連接埠。如果您在執行 Lync Server 部署精靈時未設定此 URL，則需要手動設定這些設定。系統管理員通常不需要修改這些設定，因為這些是建議值和預設連接埠。

> [!NOTE]  
> 下列螢幕擷取畫面是在設定 Standard Edition Server 時擷取的，因此 [覆寫 FQDN] 選項已停用。該選項會在設定前端集區中的 Enterprise Edition Server 時啟用。



![編輯 Web 服務集區設定](images/Gg520992.fbdf5cc9-479a-463f-bb1d-53575ecdfc9d(OCS.15).jpg "編輯 Web 服務集區設定")

## 若要設定 Web 服務

1.  以 Domain Admins 群組與 RTCUniversalServerAdmins 群組成員的身分，登入安裝了拓撲產生器的電腦。

2.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

3.  在拓撲產生器中，在主控台樹狀目錄中的 **\[Standard Edition 前端伺服器\]**、**\[Enterprise Edition 前端集區\]** 和 **\[目錄集區\]** 下，選取集區名稱。用滑鼠右鍵按一下名稱，然後依序按一下 **\[編輯內容\]** 和 **\[Web 服務\]**。

4.  新增或編輯 **\[外部 Web 服務 FQDN\]**，然後按一下 **\[確定\]**。
    
    > [!WARNING]
    > 如果您有多個前端集區或前端伺服器，外部 Web 服務 FQDN 必須是唯一的。例如，如果您將前端伺服器的外部 Web 服務 FQDN 定義為 <strong>pool01.contoso.com</strong>，就無法將 <strong>pool01.contoso.com</strong> 用於另一個前端集區或前端伺服器。如果您也部署 Director，則為任何 Director 或 Director 集區定義的外部 Web 服務 FQDN 必須是唯一的，用於區分其他的 Director 或 Director 集區以及任何的前端集區或前端伺服器。


5.  確認環境中已正確設定聆聽和發行的連接埠。

6.  針對環境中的所有 Standard Edition Server、前端集區和 Director 集區，重複執行這些步驟。

7.  在主控台樹狀目錄中，按一下 **\[Lync Server 2013\]**，然後在 **\[動作\]** 窗格中，按一下 **\[發行拓撲\]**。

設定聆聽和發行連接埠時，有一些需求應注意：

  - 顯示的聆聽連接埠是每部前端伺服器上的 Internet Information Server (IIS) 所設定的連接埠。

  - IIS 的內部和外部聆聽連接埠必須不同。以外部聆聽連接埠而言，這些通常相同，因為一個代表內部 Web 流量的硬體負載平衡器，另一個代表外部 Web 流量的反向 Proxy 伺服器。

  - 您可以覆寫 前端集區、Director 或 Director 集區上的內部 Web 服務，並定義您自己的 FQDN。
    
    > [!WARNING]
    > 如果決定使用自行定義的 FQDN 來覆寫內部 Web 服務，每個 FQDN 都必須是唯一的，用於區分其他的 前端集區、Director 或 Director 集區。


  - 在反向 Proxy 或硬體負載平衡器上，必須設定發行的連接埠作為聆聽連接埠。

  - 以前端集區而言 (範例中未顯示)，內部 SIP 集區 FQDN 與內部 Web 服務 FQDN 必須不同，因為 Web 流量是經過硬體負載平衡器而來，而內部 SIP 流量則是經過 DNS 負載平衡器而來。必須符合此需求。

  - Lync Server Standard Edition 部署不需要也不允許覆寫內部 Web 服務 FQDN，因為此伺服器無法受到平衡負載。

  - 如果環境中有硬體負載平衡器同時用於內部 SIP 和 Web 流量，則拓撲產生器無法加以區別。
    
    Web 服務 FQDN 之間應可輕鬆區別；這有助於確保 URL 重新導向將用戶端指向適當的伺服器。例如，如果您有兩個 FQDN，您可能會考慮將其中一個命名為 meeting.contoso.com，並將另一個命名為 conferencing.contoso.com。如果您的 FQDN 之間有較為相似的名稱，例如 meet1.contoso.com 與 meet2.contoso.com，則比較可能發生重新導向的問題。

外部 Web 服務會搭配周邊網路中的反向 Proxy 一起運作。這樣可讓用戶端利用這些 Web 服務而從外部存取。此處設定的 FQDN 會在用戶端登入時傳送給用戶端，並在進行遠端連線時用來建立連回反向 Proxy 的 HTTPS 連線。反向 Proxy 伺服器會將外部 Web 服務 FQDN 轉到內部硬體負載平衡器，或直接轉到集區。反向 Proxy 必須能夠將外部 Web 服務 FQDN 解析為內部 Web 伺服器的 IP 位址。外部 Web 服務 FDQN 必須可在公用網際網路中受到解析。

如果內部伺服器是 Standard Edition 伺服器，則內部 FQDN 是 Standard Edition 伺服器 FQDN。如果內部伺服器是前端集區，則 FQDN 是會對內部 Web 伺服陣列伺服器進行負載平衡的硬體負載平衡器虛擬 IP (VIP)。在具有多部 Enterprise Edition Server 的前端集區中，需要硬體負載平衡器。Standard Edition Server 或單一 Enterprise Edition 前端伺服器則不需要負載平衡器。

