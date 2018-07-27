---
title: Lync Server 2013：設定反向 Proxy 伺服器
TOCTitle: 設定反向 Proxy 伺服器
ms:assetid: 00bc138a-243f-4389-bfa5-9c62fcc95132
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398069(v=OCS.15)
ms:contentKeyID: 49289890
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Lync Server 2013 的反向 Proxy 伺服器

 

_**上次修改主題的時間：** 2014-05-08_

對於 Microsoft Lync Server 2013 Edge Server 部署，周邊網路中需要有 HTTPS 反向 Proxy，外部用戶端才能在 Director 和使用者的主集區上存取 Lync Server 2013 Web 服務 (在 Office Communications Server 中稱為 *Web 元件* )。有些需要透過反向 Proxy 進行外部存取的功能包含下列項目：

  - 讓外部使用者能夠下載會議的內容。

  - 讓外部使用者能夠擴充通訊群組。

  - 讓遠端使用者能夠從通訊錄服務下載檔案。

  - 存取 Lync Web App 用戶端。

  - 存取 \[電話撥入式會議設定\] 網頁。

  - 讓外部裝置能夠連線至裝置更新 Web 服務並取得更新。

  - 讓行動應用程式能夠自動從網際網路探索與使用行動 (Mcx) URL。

  - 讓 Lync 2013 用戶端、 Lync Windows 市集應用程式 和 Lync 2013 Mobile 用戶端能夠找到 Lync 探索 (自動探索) URL 並使用整合通訊 Web API (UCWA)。

我們建議將您的 HTTP 反向 Proxy 設定成發行所有集區中的所有 Web 服務。發行 https:// *ExternalFQDN*/\* 即可發行某個集區的所有 IIS 虛擬目錄。您組織中的每一個 Standard Edition 伺服器、前端集區 或 Director 或 Director 集區 都需要發行規則。

此外，您必須發行簡單 URL。如果組織具有 Director 或 Director 集區，則 HTTP 反向 Proxy 會聆聽簡單 URL 的 HTTP/HTTPS 要求，然後在 Director 或 Director 集區 上的外部 Web 服務虛擬目錄進行 Proxy 處理。如果您尚未部署 Director，則必須指定一個集區以處理簡單 URL 的要求 (如果這不是使用者的主集區，則會將要求向前重新導向至使用者主集區上的 Web 服務)。您可以依據專屬的 Web 發行規則處理簡單 URL，您也可以將它新增至 Director 的 Web 發行規則的公用名稱。您也需要發行外部自動探索服務 URL。

您可以使用 Microsoft Forefront Threat Management Gateway 2010、 Microsoft Internet Security and Acceleration (ISA) Server 2006 SP1 或具有 Application Request Routing (IIS ARR) 的 Internet Information Server 7.0、7.5 或 8.0 作為反向 Proxy。這一節中的詳細步驟說明如何設定 Forefront Threat Management Gateway 2010，而且用於設定 ISA Server 2006 的步驟幾乎相同。此外，也提供了 IIS ARR 的指引。如果您使用其他的反向 Proxy，請參閱該產品的文件，並將此處定義的需求對應至其他反向 Proxy 中的關聯功能。

> [!IMPORTANT]  
> Internet Information Server 應用程式要求路由 (IIS ARR) 是經完整測試並獲完整支援的 Lync Server 2010 和 Lync Server 2013 反向 Proxy 實作選項。Microsoft 已於 2012 年 11 月停止銷售 ForeFront Threat Management Gateway 2010 (又稱為 TMG) 的授權。TMG 仍是具備完整支援的產品，且仍可搭配協力廠商所售之應用裝置銷售。此外，多種協力廠商硬體負載平衡器與防火牆也提供反向 Proxy 支援。如需提供反向 Proxy 功能之硬體負載平衡器與防火牆的相關資訊，請洽詢廠商以取得有關如何設定產品以針對 Lync Server 提供反向 Proxy 支援的特定指示。您也可以查看已提交產品文件給 Microsoft 的協力廠商。協力廠商會針對本身的解決方案提供支援。若要查看目前提供解決方案的協力廠商，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=268730">Microsoft Lync 適用的基礎結構</a> (英文)。



下列主題和程序使用 Forefront Threat Management Gateway 2010 和 IIS ARR 作為部署和設定程序的基礎。

  - [針對 Lync Server 2013 設定 Web 伺服陣列 FQDN](lync-server-2013-configure-web-farm-fqdns.md)

  - [在 Lync Server 2013 中設定網路介面卡](lync-server-2013-configure-network-adapters.md)

  - [在 Lync Server 2013 中要求及設定反向 HTTP Proxy 的憑證](lync-server-2013-request-and-configure-a-certificate-for-your-reverse-http-proxy.md)

  - [在 Lync Server 2013 中設定單一內部集區的 Web 發佈規則](lync-server-2013-configure-web-publishing-rules-for-a-single-internal-pool.md)

  - [在 Lync Server 2013 中的 IIS 虛擬目錄上確認或設定驗證和憑證](lync-server-2013-verify-or-configure-authentication-and-certification-on-iis-virtual-directories.md)

  - [在 Lync Server 2013 中建立反向 Proxy 伺服器的 DNS 記錄](lync-server-2013-create-dns-records-for-reverse-proxy-servers.md)

  - [在 Lync Server 2013 中確認透過您的反向 Proxy 進行存取](lync-server-2013-verify-access-through-your-reverse-proxy.md)

## 開始之前

若要順利將 Forefront Threat Management Gateway 2010 部署成您的反向 Proxy，您必須安裝及設定伺服器，並使用 Forefront Threat Management Gateway 2010 文件中定義的先決條件和硬體需求。請參閱下列主題集以在伺服器上適當設定硬體並安裝 Forefront Threat Management Gateway 2010，再繼續進行。

   [Forefront Threat Management Gateway (TMG) 2010](http://technet.microsoft.com/zh-tw/library/ff355324.aspx)

   [Forefront TMG 2010 硬體建議事項](http://technet.microsoft.com/library/ff382651.aspx)

若要將 IIS ARR 順利部署為您的反向 Proxy，請檢視下列主題以設定硬體和必要軟體。

   若要在 Windows Server 2008 或 Windows Server 2008 R2 上安裝 IIS，請參閱＜ [在 Windows Server 2008 或 Windows Server 2008 R2 上安裝 IIS 7](http://go.microsoft.com/fwlink/?linkid=291296)＞(英文)

   若要在 Windows Server 2012 上安裝 IIS，請參閱＜ [在 Windows Server 2012 上安裝 IIS 8](http://go.microsoft.com/fwlink/?linkid=291297)＞(英文)

   如要在 Windows Server 2012 R2 上安裝 IIS，請參閱 [在 Windows Server 2012 R2 上安裝 IIS 8.5](http://go.microsoft.com/fwlink/?linkid=330687)

   若要下載 IIS Application Request Routing 延伸模組，請依照＜ [Application Request Routing v2.5 下載](http://go.microsoft.com/fwlink/?linkid=291298)＞(英文) 中的指示進行

   若要安裝 ARR，請於＜ [安裝 Application Request Routing V2](http://go.microsoft.com/fwlink/?linkid=291299)＞(英文) 取得相關指示
    
    > [!NOTE]  
    > 目前發佈的指示適用於 ARR 2.0。在延伸模組安裝方面，兩個版本間並沒有差異。
    

