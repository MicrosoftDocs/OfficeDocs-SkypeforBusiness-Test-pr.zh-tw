---
title: Lync Server 2013：自動探索服務需求
TOCTitle: 自動探索服務需求
ms:assetid: 0ac5dbf7-9acd-4d25-b21a-932022b8b983
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690012(v=OCS.15)
ms:contentKeyID: 49290046
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的自動探索服務需求

 

_**上次修改主題的時間：** 2013-02-25_

Microsoft Lync Server 2013 自動探索服務會在 Director 和前端集區伺服器上執行，而且在 DNS 中發行時，可供執行 Lync Mobile 的行動裝置用來尋找行動服務。您需要先在任何執行自動探索服務的 Director 和 前端伺服器上修改憑證主體替代名稱清單，執行 Lync Mobile 的行動裝置才能利用自動探索。此外，可能還需要針對在反向 Proxy 上用於外部 Web 服務發行規則的憑證，修改主體替代名稱清單。

如需 Director、前端伺服器和反向 Proxy 所需之主體替代名稱項目的詳細資訊，請參閱＜行動規劃＞中的＜ [Lync Server 2013 行動技術需求](lync-server-2013-technical-requirements-for-mobility.md)＞。

有關在反向 Proxy 上使用主體替代名稱清單的決策，取決於您是在連接埠 80 還是連接埠 443 上發行自動探索服務：

  - **發行在連接埠 80 上**   如果對自動探索服務的初始查詢是透過連接埠 80 來進行，則不需要任何憑證變更。這是因為執行 Lync 的行動裝置會從連接埠 80 外部存取反向 Proxy，然後在連接埠 8080 內部重新導向至 Director 或 前端伺服器。如需詳細資訊，請參閱本主題稍後的＜使用連接埠 80 的初始自動探索程序＞。

  - **發行在連接埠 443 上**   外部 Web 服務發行規則所使用之憑證上的主體替代名稱清單，必須針對組織內的每個 SIP 網域，各包含一個 *lyncdiscover.\<sipdomain\>* 項目。

使用內部憑證授權單位來重新發出憑證通常是個簡單的程序，但是針對用於 Web 服務發行規則的公用憑證，新增多個主體替代名稱項目會變得很昂貴。為解決這個問題，我們支援透過連接埠 80 的初始自動探索連線，然後再重新導向至 Director 或 前端伺服器上的連接埠 8080。

例如，假設執行 Lync Mobile 的行動用戶端設定為使用自動探索功能來登入 Lync Server 2013，以使用 HTTP 來進行初始要求。

## 使用連接埠 80 初始行動裝置的自動探索程序

1.  執行 Lync Mobile 的行動裝置會使用 A 記錄所在的 DNS 來查閱 lyncdiscover.contoso.com。

2.  外部 DNS 會將外部 Web 服務的 IP 位址傳回至用戶端。

3.  執行 Lync Mobile 的行動裝置會將要求 http://lyncdiscover.contoso.com?sipuri=lyncUser1@contoso.com 傳送至反向 Proxy。

4.  網頁發行規則會將要求從連接埠 80 外部橋接至連接埠 8080 內部，以將要求路由傳送至 Director 或 前端伺服器。
    
    由於要求是 HTTP 而不是 HTTPS，所以不需要修改外部 Web 服務發行規則的憑證來支援自動探索服務。

5.  自動探索服務會傳回外部 Web 服務 URL (以 HTTPS 格式)。

6.  然後執行 Lync Mobile 的行動裝置可以重新連線至連接埠 443 上的反向 Proxy，並透過 4443 重新導向至在使用者主集區上執行的行動服務。
    
    由於 HTTPS 查詢是針對外部 Web 服務 URL 對自動探索服務 URL，所以會成功，因為憑證已包含外部 Web 服務完整網域名稱 (FQDN) 的主體替代名稱項目。
    
    在此情況下，不需要變更憑證以支援行動性。
    
    > [!Note]  
	> 如果目標 Web 伺服器的憑證沒有 lyncdiscover.contoso.com 的相符值，以作為主體替代名稱清單值，則：<br />
    > a.   Web 伺服器會回應「伺服器問候語」，而沒有憑證。<br />
    > b.   執行 Lync Mobile 的行動裝置會立即終止工作階段。<br />
    如果目標 Web 伺服器的憑證包含 lyncdiscover.contoso.com，以作為主體替代名稱清單值，則：<br />
    > a.   Web 伺服器會回應「伺服器問候語」和憑證。<br />
    > b.   執行 Lync Mobile 的行動裝置會驗證憑證，並完成信號交換。
    


若要使用反向 Proxy 伺服器上的連接埠 80 來支援初始連線至自動探索服務，您可以建立 http 發行規則，類似用於 Forefront Threat Management Gateway 2010 反向 Proxy 網頁發行規則的下列範例：

1.  建立新的網頁發行規則 (例如， **Lync Server 自動探索 (HTTP)** )。

2.  在 \[公用名稱\] 中，輸入 lyncdiscover.contoso.com。

3.  在 \[橋接\] 索引標籤中，只選取將要求從連接埠 80 橋接至連接埠 8080 的選項。

4.  在 \[驗證\] 索引標籤上，選取 \[無驗證\] 和 \[用戶端無法直接驗證\] 。

5.  確定變更，並將規則移至 Lync 規則清單頂端 (處理順序的第一項)。

## 分割網域部署的行動性

共用 SIP 位址空間 (也稱為「分割網域」 ) 或「混合式部署」 是一種跨內部部署與線上環境來部署使用者的設定。預期的結果是要讓使用者 (無論其主伺服器是位在內部部署或線上) 登入部署，並重新導向至其主伺服器位置。為完成此作業，會使用 Microsoft Lync Server 2013 的自動探索功能來將線上使用者重新導向至線上拓撲。執行此作業需使用 Lync Server 管理命令介面以及 **Get-CsHostingProvider** 和 **Set-CsHostingProvider** Cmdlet 來設定自動探索統一資源定位器 (URL)。

您需要收集和記錄下列部署的屬性：

  - 在 Lync Server 管理命令介面中輸入：
    
        Get-CsHostingProvider

  - 在結果中尋找具有 **ProxyFQDN** 屬性的線上提供者。例如，sipfed.online.lync.com

  - 記錄 ProxyFQDN 的值

  - 在內部部署 Lync Server 控制台中啟用同盟，允許與線上提供者同盟

  - 為線上提供者啟用同盟。依預設，所有線上使用者都會啟用網域同盟，並可與所有網域通訊

  - 如果您將會定義封鎖及允許的網域，請決定您要明確允許或封鎖的網域

  - 若為線上同盟，您必須規劃防火牆例外、憑證及 DNS 主機 (若使用 IPv6，則為 A 或 AAAA) 記錄。此外，您必須設定同盟原則。如需詳細資訊，請參閱＜ [規劃 Lync Server 與 Office Communications Server 同盟](lync-server-2013-planning-for-lync-server-and-office-communications-server-federation.md)＞

