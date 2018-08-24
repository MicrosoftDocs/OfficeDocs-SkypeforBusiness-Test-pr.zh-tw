---
title: 啟用 Exchange 2013 Outlook Web App 及 IM 整合
TOCTitle: 啟用 Exchange 2013 Outlook Web App 及 IM 整合
ms:assetid: 44d08cf0-b17d-46e1-a4f0-fcc2fe96a958
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204857(v=OCS.15)
ms:contentKeyID: 49290765
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用 Exchange 2013 Outlook Web App 及 IM 整合

 

_**上次修改主題的時間：** 2012-10-19_

若要啟用 Exchange 2013 Outlook Web Access (OWA) 與立即訊息 (IM) 整合搭配 Lync Server 2013 使用，您必須將 Exchange 2013 Client Access Server (CAS) 伺服器新增至 Lync Server 2013 拓撲做為信任的應用程式伺服器。

## 建立信任的應用程式集區

1.  啟動 Lync Server 2013 管理命令介面。

2.  執行下列 Cmdlet：
    
        Get-CsSite
    
    其會傳回建立集區所在之 siteName 的 siteID。如需詳細資訊，請參閱 Lync Server 2013 管理命令介面移轉文件 [Get-CsSite](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsSite)＞。

3.  執行下列 Cmdlet：
    
        New-CsTrustedApplicationPool -Identity <E14 CAS FQDN> -ThrottleAsServer $true -TreatAsAuthenticated $true -ComputerFQDN <E14 CAS FQDN> -Site <Site> -Registrar <Pool FQDN in the site> -RequiresReplication $false
    
    如需詳細資訊，請參閱 Lync Server 2013 管理命令介面移轉文件 [New-CsTrustedApplicationPool](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsTrustedApplicationPool)＞。
    
    Exchange Server FQDN 應設定為 Exchange OWA 憑證主體名稱 (SN)，或主體別名 (SAN)。
    
    在 Exchange OWA 中，確認集區的 FQDN 也是可信任的。
    
    > [!IMPORTANT]  
    > 如果您的 CAS 伺服器 <em>沒有</em> 組合在執行 Exchange 2013 Unified Messaging (UM) 的同一部伺服器上，請略過本程序中的其餘步驟，並執行本主題中稍後的＜為 Exchange 2013 CAS 伺服器建立信任的應用程式＞程序。 若您的 CAS 伺服器組合在執行 Exchange 2013 Unified Messaging (UM) 的同一部伺服器上，請完成本程序中的步驟，而不要執行本主題中稍後的＜為 Exchange 2013 CAS 伺服器建立信任的應用程式＞程序。
    


4.  執行 **\[Enable-CsTopology\]** 。

5.  開啟 Topology Builder，然後下載現有的拓樸。

6.  在左邊的窗格中，展開樹狀目錄，直到找到 **\[信任的應用程式伺服器\]** 。

7.  展開 **\[信任的應用程式伺服器\]** 節點。

8.  現在您應該會看到 Exchange 2013 CAS 伺服器列為信任的應用程式伺服器。

## 建立 Exchange 2013 CAS 伺服器的信任的應用程式

1.  啟動 Lync Server 2013 管理命令介面。

2.  如果您的 CAS 伺服器 *沒有* 組合在執行 Exchange 2013 Unified Messaging (UM) 的同一部伺服器上，請執行下列 Cmdlet：
    
        New-CsTrustedApplication -ApplicationId <AppID String> -TrustedApplicationPoolFqdn <E14 CAS FQDN> -Port <available port number>
    
    如需詳細資訊，請參閱＜ Lync Server 2013 管理命令介面＞移轉文件 [New-CsTrustedApplication](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsTrustedApplication)＞主題。

3.  執行 **\[Enable-CsTopology\]** 。

4.  從拓撲產生器，在左邊的窗格中，展開樹狀目錄，直到找到 **\[信任的應用程式伺服器\]** 。

5.  展開 **\[信任的應用程式伺服器\]** 節點。

6.  現在您應該會看到 Exchange 2013 CAS 伺服器列為信任的應用程式伺服器。

