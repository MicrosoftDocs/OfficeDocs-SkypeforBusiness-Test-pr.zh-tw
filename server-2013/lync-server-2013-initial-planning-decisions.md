---
title: Lync Server 2013 初始規劃決策
TOCTitle: 初始規劃決策
ms:assetid: cbaa5cb3-2b00-4b9f-952d-986a0c9f160b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398855(v=OCS.15)
ms:contentKeyID: 49292330
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的初始規劃決策

 

_**上次修改主題的時間：** 2012-10-01_

規劃程序的第一部分是確定貴組織所需的 Lync Server 工作負載和主要功能。

1.  **想要採用內部部署還是線上部署？**   
Lync Server 可支援這兩種部署案例。如需關於進行此決策的詳細資訊，請參閱本節稍早的 [決定 Lync Server 2013 的部署方式](lync-server-2013-deciding-how-to-deploy-microsoft-lync.md)

2.  **想要採用實體拓撲還是虛擬拓撲？**   
Lync Server 可支援實體拓撲與虛擬拓撲中的所有工作負載和伺服器角色。實體拓撲與虛擬拓撲中的使用者容量和延展性可能會不同。如需詳細資訊，請參閱 [在虛擬伺服器上執行 Lync Server](lync-server-2013-running-lync-server-on-virtual-servers.md)。

3.  **立即訊息 (IM) 和「目前狀態」 一律會啟用。** 在任何 Lync Server 部署中，預設都會安裝並啟用立即訊息 (IM) 和顯示狀態工作負載。透過 IM，使用者可以利用即時文字訊息彼此通訊，而透過目前狀態，使用者可以檢視網路中其他使用者的狀態。使用者提供的目前狀態資訊讓其他使用者可以確定是否要嘗試聯絡這位使用者以及如何聯絡。如需詳細資訊，請參閱規劃文件中的 [在 Lync Server 2013 中規劃前端伺服器、立即訊息及顯示狀態](lync-server-2013-planning-for-front-end-servers-instant-messaging-and-presence.md)。

4.  **是否要部署任何模式的會議？**   
會議是 Lync Server 的另一項核心功能。支援的會議模式有數種。您可以選擇部署所有受支援類型的會議，也可以選擇僅部署部分類型的會議。透過「Web 會議」 ，使用者可以檢視正在簡報的檔案，例如採用 Microsoft PowerPoint 簡報圖形程式建立的投影片。透過「應用程式共用」 ，使用者可以即時相互共用自己的整個或部分桌面。憑藉「A/V 會議」 ，使用者可以在會議和對等通訊中新增音訊 (甚至是視訊)。透過「電話撥入式會議」 ，使用者可以使用標準 PSTN 電話加入貴組織舉辦的會議之音訊部分。如需詳細資訊，請參閱規劃文件中的 [Lync Server 2013 中的會議規劃](lync-server-2013-planning-for-conferencing.md)。
    
    在 Lync Server 2013 中，如果您部署 Web 會議，則也必須規劃 Office Web Apps Server 整合，以便在會議中能夠進行 Powerpoint 分享和檢視。如需詳細資訊，請參閱 [設定 Office Web Apps Server 與 Lync Server 2013 的整合](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md)。

5.  **部署 A/V 會議時，還應該監控這些會議的音訊品質。** 許多因素都會影響 Lync Server A/V 會議的音訊和視訊品質。透過監控的使用，您可以監控通話和會議的 A/V 品質。您可以偵測影響媒體品質的問題，確保使用者獲得最佳的媒體經驗。如需詳細資訊，請參閱 [Lync Server 2013 中的規劃監控](lync-server-2013-planning-for-monitoring.md)。

6.  **是否要讓 IM 伺服器、目前狀態伺服器和會議伺服器展現高度可用性？**   
如果您某個網站中只使用一部伺服器來提供 IM、顯示狀態和會議功能，萬一該伺服器故障，使用者的產能會受到嚴重影響。透過部署至少含有三部伺服器來負責這些功能的 Enterprise Edition 集區 ，即使其中一部伺服器無法使用， Lync Server 仍可繼續運作，而且所有這些功能完全不受影響。
    
    使用者人數在 5000 人以內的組織如果想要高可用性有另一個選項，就是部署兩部執行 Lync ServerStandard Edition 的伺服器，並將這些伺服器配對在一起。如需詳細資訊，請參閱 [在 Lync Server 2013 中規劃高可用性和災害復原](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)。

7.  **是否要有災害復原選項？**  
如果您有兩個資料中心，且想要有災害復原選項好讓使用者在一個資料中心裡的全部或許多伺服器故障時能夠繼續工作，您可以在部署伺服器時考量到災害復原。在此部署中，您將某個資料中心裡的伺服器集區與另一個資料中心裡的對應集區相配對。如果其中一個資料中心故障，配對中的另一個集區便可以同時服務兩個集區裡的使用者，將服務中斷的影響降至最低。如需詳細資訊，請參閱 [在 Lync Server 2013 中規劃高可用性和災害復原](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)。

8.  **是否要讓您的使用者與外部使用者通訊和共同作業？**  
讓使用者與外部使用者通訊和共同作業可以增加 Lync Server 的投資報酬率。這樣，貴組織自己的使用者即使在組織的防火牆外工作，仍然可以享有 Lync Server 功能。您也可以與執行 Lync Server 的工作夥伴或客戶組織建立同盟。如此一來，您的使用者和同盟協力廠商使用者就可以輕鬆地傳送和接收 IM 訊息、邀請彼此參加自己的會議，以及查看彼此的目前狀態。此外，您的使用者可以使用電子郵件訊息邀請特定的外部使用者來參加自己召集的會議。如需詳細資訊，請參閱 [在 Lync Server 2013 中規劃外部使用者存取](lync-server-2013-planning-for-external-user-access.md)。

9.  **是否要部署 Enterprise Voice？**  
「Enterprise Voice」 是 Lync Server 提供的 Voice over IP (VoIP) 解決方案。VoIP 為傳統式 PBX 電話語音提供吸引人的替代方案。透過 Enterprise Voice，使用者可以在自己的電腦或 VoIP 電話上按一下 Outlook 或 Lync Server 聯絡人來撥打電話。使用者還可以透過 IP 網路，撥打電腦對電腦、電腦對電話機、電話機對電腦的電話。使用者從他們的電腦即可使用所有整合的通訊選項 (語音、電子郵件、IM 和會議)，獲得更好的通訊經驗。如需詳細資訊，請參閱規劃文件中的 [在 Lync Server 2013 中規劃企業語音](lync-server-2013-planning-for-enterprise-voice.md)。

10. **部署 Enterprise Voice 時，還需要監控通話的音訊品質。** 我們建議您使用監控以確保 Enterprise Voice 通話的音訊品質 (如果部署有 Enterprise Voice)。如需詳細資訊，請參閱 [Lync Server 2013 中的規劃監控](lync-server-2013-planning-for-monitoring.md)。

11. **是否需要針對規範用途封存 IM 內容或會議內容？**  
如果貴組織需要針對規範用途封存 IM 內容或會議內容，則可以部署封存。如需詳細資訊，請參閱 [在 Lync Server 2013 中規劃封存](lync-server-2013-planning-for-archiving.md)。

12. **是否要部署常設聊天室？**  
如果您想要讓使用者能進行長期持續的即時交談，您可以部署常設聊天室。如需詳細資訊，請參閱 [在 Lync Server 2013 中規劃常設聊天室伺服器](lync-server-2013-planning-for-persistent-chat-server.md)。


13. **是否已部署 Microsoft Exchange？**  如果貴組織使用 Microsoft Exchange Server 提供電子郵件服務，您可以啟用數項功能來加強 Lync Server 和 Microsoft Exchange Server 的實用性。部分這些功能 (稱為 Exchange 整合通訊 (UM)) 包括：讓使用者從 Outlook 或 Outlook Web Access 接收語音信箱通知和聆聽語音信箱訊息、從電話機存取 Microsoft Exchange 信箱，以及在 Microsoft Exchange 信箱中接收傳真。此外，如果您部署了 Exchange 2013，您可以整合使用者在這兩個系統中的連絡人存放區、使用 Exchange 存放較高解析度的連絡人相片，以及整合電子郵件與立即訊息的封存。如需詳細資訊，請參閱 [規劃 Exchange Server 整合](lync-server-2013-planning-for-exchange-server-integration.md)。

14. **貴組織中是否有分公司？**  
如果貴組織有分公司， Lync Server 有各種方式可支援這些分公司，並確保它們享有語音與其他功能的恢復能力。特別是在沒有可恢復的 WAN 連結來連到資料中心的分公司中，您可以安裝 Survivable Branch Appliance 或 Survivable Branch Server，以在廣域網路 (WAN) 連結不通時仍保有 Enterprise Voice 支援。如需詳細資訊，請參閱 [在 Lync Server 2013 中規劃分支網站語音彈性](lync-server-2013-planning-for-branch-site-voice-resiliency.md)。

