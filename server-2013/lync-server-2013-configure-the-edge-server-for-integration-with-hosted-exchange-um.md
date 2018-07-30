---
title: Lync Server 2013：將 Edge Server 設定為與主控 Exchange UM 整合
TOCTitle: 將 Edge Server 設定為與主控 Exchange UM 整合
ms:assetid: ede3f2f9-f412-418e-a705-8d8ec98176c5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399075(v=OCS.15)
ms:contentKeyID: 49292722
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將 Edge Server 設定為與主控 Exchange UM 整合

 

_**上次修改主題的時間：** 2015-01-23_

若要在託管的 Exchange 整合通訊 (UM) 上為 Lync Server 2013 使用者提供語音信箱功能，您必須在 Edge Server 上執行下列設定工作：

  - 設定同盟的 Edge Server。

  - 將 中央管理存放區資料複寫到 Edge Server 並確認複寫。

  - 在 Edge Server 上建立裝載提供者。

如需詳細資訊，請參閱 Lync Server 管理命令介面文件中關於下列 Cmdlet 的部分：

  - [Set-CsAccessEdgeConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsAccessEdgeConfiguration)

  - [New-CsHostingProvider](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsHostingProvider)

> [!IMPORTANT]  
> 您必須針對裝載的 Exchange 服務建立外部 DNS SRV 記錄，再執行這些步驟。如需詳細資訊，請參閱＜ <a href="lync-server-2013-create-a-dns-srv-record-for-integration-with-hosted-exchange-um.md">針對與主控 Exchange UM 的整合建立 DNS SRV 記錄</a>＞。



## 若要設定同盟的 Edge Server

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 Set-CsAccessEdgeConfiguration Cmdlet 設定同盟的伺服器。例如，執行：
    
        Set-CsAccessEdgeConfiguration -UseDnsSrvRouting -AllowFederatedUsers 1 -EnablePartnerDiscovery 0
    
    上述範例會設定下列參數：
    
      - **UseDnsSrvRouting** 指定 Edge Server 傳送和接收同盟要求時將依賴 DNS SRV 記錄。
    
      - **AllowFederatedUsers** 指定是否允許內部使用者與同盟網域的使用者進行通訊。此屬性也會判斷內部使用者是否可與分割網域案例中的使用者進行通訊。
    
      - **EnablePartnerDiscovery** 會指定 Lync Server 是否將使用 DNS 記錄嘗試探索未在 Active Directory 允許的網域清單中列出的協力廠商網域。若為 False， Lync Server 2013 將只會與允許的網域清單中的網域結盟。如果使用 DNS 服務路由，則需要此參數。在大多數部署中，此值設定為 False，以免對所有合作夥伴開放同盟。

## 若要將資料複寫到 Edge Server 並確認複寫

  - 確認複寫至 Edge Server 的作業已完成。若要瞭解相關程序，請參閱[在 Lync Server 2013 中驗證內部伺服器和 Edge Server 之間的連線](lync-server-2013-verify-connectivity-between-internal-servers-and-edge-servers.md)。

## 若要在 Edge Server 上建立裝載提供者

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 **New-CsHostingProvider** Cmdlet 以設定裝載提供者。例如，執行：
    
        New-CsHostingProvider -Identity Fabrikam.com -Enabled $True -EnabledSharedAddressSpace $True -HostsOCSUsers $False -ProxyFQDN "proxyserver.fabrikam.com" -IsLocal $False -VerificationLevel UseSourceVerification
    
    上述範例會設定下列參數：
    
      - **Identity** 會為您建立的裝載提供者指定唯一字串值識別碼，此範例中為 **Fabrikam.com** 。請注意，如果已對該 Identity 設定現有提供者，則命令會失敗。
    
      - **Enabled** 指出網域與裝載提供者之間的網路連線是否已啟用。只有將此值設為 **True** ，才能在兩個組織之間交換訊息。
    
      - **EnabledSharedAddressSpace** 會指出裝載提供者是否已在共用 SIP 位址空間 (分割網域) 案例中使用。
        
        > [!NOTE]  
        > 在將 <code>EnableSharedAddressSpace</code> 設為 True 之前，請嘗試在內部解析同盟 SRV 記錄。如果此記錄無法於內部解析，接著您需要在內部 DNS 中建立 _sipfederationtls._tcp.&lt;domain&gt; 和 _sip._tls.&lt;domain&gt; 的記錄。這些記錄應指向 Edge Server 的 Access 介面的外部 IP 位址。
        
    
      - **HostsOCSUsers** 指出裝載提供者是否用於裝載 Lync Server 2013 帳戶。如果為 **False** ，則提供者會裝載其他帳戶類型，例如 Microsoft Exchange 帳戶。
    
      - **ProxyFQDN** 會指定裝載提供者所使用 Proxy 伺服器的完整網域名稱 (FQDN)，此範例中為 **proxyserver.fabrikam.com** 。您無法修改此值。如果裝載提供者變更其 Proxy 伺服器，則您必須刪除並重新建立該提供者的項目。
    
      - **IsLocal** 指出裝載提供者使用的 Proxy 伺服器是否包含在您的 Lync Server 2013 拓撲內。
    
      - **VerficationLevel** 指出傳送至裝載提供者或從裝載提供者發出之訊息的允許驗證層級。指定 **UseSourceVerification**，其依賴包含在裝載提供者發出之訊息內的驗證層級。如果沒有指定這個層級，訊息會視為無法驗證而被拒絕。

## 請參閱

#### 工作

[匯出 Lync Server 2013 拓撲並將拓撲複製到 Edge 安裝的外部媒體](lync-server-2013-export-your-topology-and-copy-it-to-external-media-for-edge-installation.md)  

#### 概念

[在 Lync Server 2013 中驗證內部伺服器和 Edge Server 之間的連線](lync-server-2013-verify-connectivity-between-internal-servers-and-edge-servers.md)  

#### 其他資源

[New-CsHostingProvider](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsHostingProvider)

