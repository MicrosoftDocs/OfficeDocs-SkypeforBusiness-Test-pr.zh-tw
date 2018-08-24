---
title: 為 Lync Online 網域設定同盟支援
TOCTitle: 為 Lync Online 網域設定同盟支援
ms:assetid: 19d5d5be-cd7f-47b8-b6c5-651a3191def7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202166(v=OCS.15)
ms:contentKeyID: 49290239
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 為 Lync Online 網域設定同盟支援

 

_**上次修改主題的時間：** 2012-11-01_

與 Microsoft Lync Online 2010 客戶同盟需要完成下列步驟：

  - 設定 Lync Online 2010 客戶的網域支援 (例如，contoso.onmicrosoft.com)。如同本文件的＜[與 Lync Online 客戶同盟的先決條件](lync-server-2013-prerequisites-for-federating-with-a-lync-online-customer.md)＞一節所述，您應該已經為組織啟用同盟。啟用同盟需要指定同盟網域用來控制存取的方法。如果您將組織設定成使用探索，則可選擇是否將網域新增至組織的允許清單中。如果您未啟用網域探索，則必須將 Lync Online 客戶的網域名稱新增至您的允許網域清單中。您可以使用 Lync Server 控制台或執行 **New-CSAllowedDomain** Cmdlet，來新增網域名稱。如需使用 Lync Server 控制台的詳細資訊 (包括啟用網域探索)，請參閱作業文件中的＜[在 Lync Server 2013 中管理組織的 SIP 同盟提供者](lync-server-2013-manage-sip-federated-providers-for-your-organization.md)＞。如需使用 **New-CSAllowedDomain** Cmdlet 來新增網域的詳細資訊，請參閱作業文件中的＜[New-CsAllowedDomain](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsAllowedDomain)＞。
    
    > [!NOTE]  
    > Lync Online 客戶可以擁有多個網域。如果您想與一個以上的網域同盟，必須為每個您想支援同盟的個別網域設定相關支援，而且 Lync Online 客戶的管理員必須為要同盟的每個網域啟用同盟。
    


  - 針對您想同盟之 Lync Online 2010 客戶網域的裝載提供者設定支援。請使用本節中的程序，為裝載提供者設定相關支援。
    
    > [!NOTE]  
    > 只有在與 Lync Online 客戶的網域同盟時，才需要此步驟，要與同盟協力廠商位置上內部部署的任何網域同盟時，則不需要此步驟。
    


## 針對裝載提供者設定支援

1.  從前端伺服器，啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 **New-CsHostingProvider** Cmdlet，以建立和設定裝載提供者。例如，執行：
    
        New-CsHostingProvider -Identity LyncOnline -ProxyFqdn "sipfed.online.lync.com" -VerificationLevel UseSourceVerification -Enabled $True -EnabledSharedAddressSpace $False -HostsOCSUsers $False -IsLocal $False
    
    上述範例會設定下列參數：
    
      - **Identity** 會為您建立的裝載提供者指定唯一字串值識別碼。請注意，如果已對該 Identity 設定現有提供者，則命令會失敗。
    
      - **ProxyFQDN** 會指定裝載提供者所使用 Proxy 伺服器的完整網域名稱 (FQDN)。您無法修改此值。如果裝載提供者變更其 Proxy 伺服器，則您必須刪除並重新建立該提供者的項目。
    
      - **VerificationLevel** 會指定如何驗證 (或是否驗證) 從裝載提供者傳送的訊息，以確認它們確實是傳送自該提供者。
    
      - **Enabled** 會指出網域和裝載提供者之間的網路連線是否已啟用。只有將此值設為 **True**，才能在兩個組織之間交換訊息。
    
      - **EnabledSharedAddressSpace** 會指出裝載提供者是否已在共用 SIP 位址空間 (分割網域) 案例中使用。
    
      - **HostsOCSUsers** 會指出裝載提供者是否用於主控 Lync Server 帳戶。如果為 **False**，則提供者會主控其他帳戶類型，例如 Microsoft Exchange 帳戶。
    
      - **IsLocal** 會指出裝載提供者使用的 Proxy 伺服器是否包含在您的 Lync Server 拓撲內。
    
    如需有關使用此 Cmdlet 的詳細資訊，請參閱作業文件中的＜[New-CsHostingProvider](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsHostingProvider)＞。

