---
title: 使用 Lync Connectivity Analyzer
TOCTitle: 使用 Lync Connectivity Analyzer
ms:assetid: 954953fb-0c7a-4fd5-8acd-68ecb59b20af
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ907302(v=OCS.15)
ms:contentKeyID: 52056151
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用 Lync Connectivity Analyzer

 

_**上次修改主題的時間：** 2014-02-11_

Microsoft Lync 連線分析程式可協助 Lync 糸統管理員判定其 Office 365 或內部部署 Lync Server 環境的部署與設定是否符合需求，以支援行動裝置上來自 Lync Windows 市集應用程式 和 Lync 應用程式的連線。

Lync 連線分析程式嘗試利用與 Lync Windows 市集應用程式和 Lync 行動應用程式所使用之相同的服務與通訊協定連線至 Lync Server 內部部署或 商務用 Skype Online。您可以在連線至 Lync Server 或 商務用 Skype Online 的內部網路與外部網路中執行連線測試。Lync 連線分析程式會提供一份報告，內含關於每一個連線步驟的詳細資訊，以協助您驗證組態並疑難排解連線問題。

Lync 連線分析程式測試以下 Lync Server 元件：

  - Autodiscover 服務

  - Authentication Broker (Reach) 服務

  - Mobility (MCX) 服務

  - Mobility (UCWA) 服務

  - WebTicket 服務

Lync 連線分析程式測試以下其他元件的組態：

  - 適用於自動探索 URL 的 DNS 記錄的發佈

  - 憑證

  - Proxy 伺服器

您可以從 Microsoft 下載中心下載 Lync 連線分析程式，網址為：<http://go.microsoft.com/fwlink/?linkid=277056>。

## 分析您的連線

1.  對於要用來測試連線之工具會使用的有效 Lync 帳戶 (內部部署的 Lync 帳戶或 Office 365Lync 帳戶)，請輸入認證：
    
      - 在 \[Lync 帳戶類型\] 中，選取 \[Office 365\] 或 \[內部部署\]。
    
      - 在 \[SIP URI\] 中，輸入 Lync 連線的 SIP 登入位址，格式為 \[user@domain.com\]。
    
      - 在 \[密碼\] 中，輸入與此帳戶相關的密碼。
    
      - 在 \[使用者名稱 (選用)\] 中，輸入使用者名稱 (如果適用的話)。使用者名稱又稱為「使用者主要名稱」(UPN)。如果使用者名稱和 SIP URI 相同，則不需要輸入使用者名稱。如果不同，請以格式 \[user@domain.com\] 或 \[domain\\user\] 輸入使用者名稱 (如果適用的話)。
    
      - 如果從連線至內部網路的電腦執行 Lync 連線分析程式，請在 \[網路存取\] 選擇 \[從我的組織內部\]。否則，請選擇 \[外部 (網路)\]。Lync 連線分析程式一律會執行內部和外部測試，但若指定您是在所屬網路的內部或外部，可協助工具解譯是否預料有某些失敗。
    
      - 在 \[用戶端\] 下，選取是否為 \[Lync Windows 市集應用程式\]、\[Lync Mobile 2010 應用程式\] 或 \[Lync Mobile 2013 應用程式\] 執行連線測試。
    
      - 在 \[伺服器探索\] 下，選取要執行的測試類型：
        
          - 如果您希望工具能自動探索 Lync Server，請選取 \[自動\]。
        
          - 如果您希望工具忽略自動探索測試，或如果您知道要連線的伺服器名稱，請選取 \[手動使用位址:\]，然後指定 Lync 伺服器的完整網域名稱 (FQDN)，例如 **lync.company.com**。

2.  (選用) 在 \[記錄檔\] 下，如要在指定的路徑建立記錄檔，請選取核取方塊。如已啟用記錄功能，按一下 \[清除\] 可清除記錄檔，按一下 \[開啟\] 可開啟和查看記錄檔，按一下 \[電子郵件\] 可開啟電子郵件訊息，將結果傳送給支援小組 (您必須從指定的路徑手動附加記錄檔)。

3.  按一下 \[啟動\]。

下列功能顯示來自 Lync 連線分析程式的範例結果。

**Lync 連線分析程式**

![Lync 連線分析程式的螢幕擷取畫面](images/JJ907302.a7cc0abe-fac2-4691-a7d8-9ffef59cdee5(OCS.15).png "Lync 連線分析程式的螢幕擷取畫面")

## 由 Lync 連線分析程式測試的元件

Lync 連線分析程式嘗試使用 Lync Windows 市集應用程式和 Lync 行動應用程式探索 Lync 伺服器並建立連線。它會依照本節所述來執行測試。

如果已選取 \[自動探索\]，則 Lync 連線分析程式會執行下列動作：

  - 針對自動探索 URL 查詢網域名稱服務。

  - 使用安全的內部通道嘗試探索。例如，\[HTTPS://lyncdiscoverinternal.company.com/\]。

  - 使用不安全的內部通道嘗試探索。例如，\[HTTP://lyncdiscoverinternal.company.com/\]。

  - 使用安全的外部通道嘗試探索。例如，\[HTTPS://lyncdiscover.company.com\]。

  - 使用不安全的外部通道嘗試探索。例如，\[HTTP://lyncdiscover.company.com\]。

如果已選取 \[使用以下伺服器探索位址\]，則 Lync 連線分析程式會執行下列動作：

  - 針對伺服器的 FQDN 查詢 DNS。

  - 使用安全的通道嘗試探索。例如，\[HTTPS://serverFQDN/\]。

  - 使用不安全的通道嘗試探索。例如，\[HTTP://serverFQDN/\]。

如果已選取 \[測試需求\] 之下的 \[Lync Windows Store 應用程式\]，則 Lync 連線分析程式會執行下列動作：

  - 驗證是否可使用 WebTicket 服務，並測試 Lync 帳戶認證的授權。

  - 驗證是否可使用 Authentication Broker (Reach) 服務。

如果在 \[用戶端\] 下已經選取 \[Lync Mobile 2010 應用程式\]，Lync 連線分析程式會執行下列動作：

  - 驗證是否可使用 WebTicket 服務，並測試 Lync 帳戶認證的授權。

  - 驗證是否可使用 Mobility (MCX) 服務。

如果已選取 \[用戶端\] 下的 \[Lync Mobile 2013 應用程式\]，則 Lync 連線分析程式會執行下列動作：

  - 驗證是否可使用 WebTicket 服務，並測試 Lync 帳戶認證的驗證。

  - 驗證 Mobility (UCWA) 服務是否可用。

執行這些測試時，Lync 連線分析程式會驗證 Lync Server、硬體負載平衡器、Proxy 伺服器，以及在執行測試的電腦上的認證。

## 其他資源

Microsoft 也提供 Microsoft 遠端連線分析程式 (一種 Web 連線測試工具)，可透過以下網址取得：<https://testconnectivity.microsoft.com/>。Lync 連線分析程式和遠端連線分析程式在以下方面有所不同：

  - 遠端連線分析程式可針對 Microsoft Exchange 和 Outlook 測試連線，除了 Microsoft Lync 以外。

  - 遠端連線分析程式可完成 SIP 登入，而 Lync 連線分析程式僅驗證帳戶認證，而不登入。

  - 遠端連線分析程式只會從組織網路的外部測試連線，因為它是從公用 Web 伺服器執行。

  - 遠端測試分析程式不會測試 Authentication Broker (Reach)、Mobility (MCX) 和 WebTicket 服務的可用性。

  - Lync 連線測試程式會測試自動探索服務。

  - 遠端連線分析程式可連線至 Lync Server 的任何版本，而 Lync 連線分析程式只能成功連線至 Lync Server 2010 (至少包含 Lync Server 2010 的累計更新：2012 年 2 月)，或 Lync Server 的最新版本。

下列文件說明部署與設定 Lync Server 以支援 Lync Windows 市集應用程式 和 Lync 行動用戶端的需求與程序：

  - [在 Lync Server 2013 中部署用戶端和裝置](lync-server-2013-deploying-clients-and-devices.md)

  - [Lync Server 2013 中的行動規劃](lync-server-2013-planning-for-mobility.md)

  - [在 Lync Server 2013 中部署行動性](lync-server-2013-deploying-mobility.md)

