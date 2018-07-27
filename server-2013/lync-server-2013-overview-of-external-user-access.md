---
title: Lync Server 2013：外部使用者存取概觀
TOCTitle: 外部使用者存取概觀
ms:assetid: 97aded6c-5fa3-4225-95a6-9ad094d61654
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398775(v=OCS.15)
ms:contentKeyID: 49291764
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的外部使用者存取概觀

 

_**上次修改主題的時間：** 2013-11-07_

在本文件中，我們使用「外部使用者」 一詞來代表從防火牆外部與 Lync Server 2013 和 Lync 2013 使用者通訊的這類大宗使用者。您可授權其使用 Lync Server 2013 與內部使用者 (亦即從防火牆內部登入 Lync Server 的使用者) 通訊的外部使用者包括：

  - **遠端使用者**   貴組織從防火牆之外登入 Lync Server 的使用者。

  - **同盟使用者**   在受信任的客戶或合作夥伴組織那邊具有帳戶 (例如 Lync Server 2010、 Lync Server 2013 或 Office Communications Server 2007 R2) 的使用者。同盟使用者也可以是已定義之合作夥伴組織的成員，這些組織透過 Edge Server 上的 XMPP Proxy 以及 前端伺服器或集區上的 XMPP 閘道來使用可延伸傳訊和顯示狀態通訊協定 (XMPP)。已定義的信任關係 (稱為同盟) 與 Active Directory 網域服務 信任關係既無關也不相依。
    
    > [!NOTE]  
    > 目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的確切結束日期。如需詳細資訊，請參閱＜ <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>＞。
    


  - **Public Instant Messaging Connectivity 使用者**   您的使用者透過公用立即訊息連線服務 (Windows Live、Yahoo\! 及 AOL) 建立的連絡人。

  - **行動使用者**   因使用智慧型手機或平板電腦上的 Lync Mobile 用戶端登入了內部部署，而能夠與其他類別的使用者進行通訊的企業內部使用者。行動使用者會使用透過反向 Proxy 公佈的行動服務來存取內部部署。如需關於 Lync Mobile 可用之功能的詳細資訊，請參閱 [http://go.microsoft.com/fwlink/?linkid=234777\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=234777%26clcid=0x404) 的「行動用戶端比較表」。

  - **匿名使用者**   在您組織的 Active Directory 網域服務 或支援的同盟網域中沒有帳戶，但受邀請從遠端參加內部部署會議的使用者。

您的邊緣部署會針對下列通訊類型提供外部存取：

  - **IM 和目前狀態**   取得授權的外部使用者能參與 IM 交談和會議，也能看見其他參與者的目前狀態。公用 IM 服務提供者的使用者可以參與對貴組織內個別 Lync Server 使用者舉行的 IM 交談並看見狀態資訊，但是無法參與以 Lync Server 舉行的 IM 多方會議。完全只能進行對等通訊。檔案傳輸功能不支援公用 IM 服務提供者的使用者，而且對等通訊中的音訊/視訊僅支援 Windows Messenger 2011 使用者，而不支援其他使用公用 IM 服務提供者的使用者。
    
    同時支援 SIP 和 XMPP 通訊協定。若要提供 XMPP 的服務，請參閱＜ [規劃 Lync Server 2013 中的 SIP、XMPP 同盟和公用立即訊息](lync-server-2013-planning-for-sip-xmpp-federation-and-public-instant-messaging.md)＞。

  - **Web 會議**   取得授權的外部使用者能參與 Lync Server 部署上裝載的會議。您可以為遠端使用者、同盟使用者及匿名使用者啟用 Web 會議的參與，但公用 IM 使用者無法參與會議。視您選取的選項而定，啟用 Web 會議的使用者能參與桌面共用和應用程式共用，也能成為會議召集人或簡報者。

  - **A/V 會議**   取得授權的外部使用者能 Lync Server 部署上裝載的音訊與視訊會議。對等通訊中的音訊/視訊可支援 Windows Messenger 2011 使用者，但是不支援其他使用公用 IM 服務提供者的使用者。

為方便控制通訊，您可以設定一個或多個原則來定義貴組織內外的使用者彼此通訊的方式。您也可以針對個別內部使用者或是特定類型的外部使用者來配置設定及套用原則，以控制與外部使用者之間的通訊。

用來提供外部存取的 Lync Server 2013 角色：

**Edge Server**    Edge Server 是一或多個伺服器，其執行的服務可允許從外部存取 IM 和目前狀態、會議、音訊/視訊及其他媒體 (例如，檔案傳輸) 服務。您可以選擇是否設定 Edge Server 來與其他 Lync Server 或 Office Communications Server 2007 R2 部署和其他 XMPP 部署建立同盟。選用的公用 IM 連線功能是透過 Edge Server 來啟用和設定。

**Director**    Director 是選用伺服器或伺服器集區，其執行 Lync Server 2013  Director角色來預先驗證使用者要求，並將要求路由至使用者所屬的 前端伺服器或 前端集區，但是不會主管任何使用者帳戶。

**反向 Proxy**   反向 Proxy 是一種特殊伺服器的通稱，這種伺服器會公佈內部網路上的可用資源，並且幫用戶端從公佈的資源擷取資訊。 Lync Server 2013 使用反向 Proxy 來公佈數項功能，例如會議、會議加入位置、通訊錄、通訊群組清單展開、會議內容下載、裝置更新、行動服務等等。任何符合公佈必要資源位置相關需求的反向 Proxy 都可以使用。為了說明公佈規則的重要性，我們使用了 Microsoft Forefront Threat Management Gateway (TMG) 2010 作為範例，但並非一定要使用 Forefront TMG 2010。

> [!IMPORTANT]  
> Lync Server 2013 同時支援 IPv4 和 IPv6。 Windows Server 2008 R2、 Windows Server 2012 和 Windows Server 2012 R2 使用了可以同時使用 IPv4 和 IPv6 的雙重堆疊。這一點相當重要，因為部署在從 IPv4 移至 IPv6 時會有一段過渡時期。也許某些區域支援 IPv4，而在部署的其他區域卻使用 IPv6。在考量網際網路與內部部署時，這點尤其要注意。外部用戶端必須透過反向 Proxy 通訊才能使用行動、會議、通訊錄下載等服務。就目前而言，Forefront Threat Management Gateway 2010 和 Internet Security and Acceleration Server 2006 不論部署於何種作業系統版本，都不支援 IPv6 定址。這點在規劃與外部用戶端有關的 IPv6 和 IPv4 使用時必須注意。


