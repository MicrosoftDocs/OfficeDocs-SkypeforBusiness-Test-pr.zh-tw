---
title: Lync Server 2013：檢視 Microsoft SIP Processing Language (MSPL) 伺服器應用程式
TOCTitle: 檢視 Microsoft SIP Processing Language (MSPL) 伺服器應用程式
ms:assetid: b7df1323-b6bd-4925-8fe6-5241c91fe51b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182575(v=OCS.15)
ms:contentKeyID: 49292098
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中檢視 Microsoft SIP Processing Language (MSPL) 伺服器應用程式

 

_**上次修改主題的時間：** 2014-09-26_

Microsoft SIP Processing Language (MSPL) 伺服器應用程式是僅限指令碼的應用程式，它會使用指令碼語言，而不是 Microsoft Lync 2010 API。MSPL 除了能夠將特定訊息分派至以交易為主的 SIP 應用程式之外，還能對篩選和 Proxy 行為提供更細微的控制。MSPL 特別適用於篩選和路由傳送 SIP 訊息。MSPL 應用程式與 UserServices 模組是在同一個處理序中執行，而以 Lync 2010 API 為主的程式則是在不同的處理序中執行。

您可以使用 Lync Server 控制台 之 \[拓撲\] 群組中的 \[伺服器應用程式\] 頁面，來查看您 Lync Server 2013 環境中前端伺服器上執行之 MSPL 伺服器應用程式的清單。此清單會顯示每個集區可使用的指令碼，以及這些指令碼是否啟用或是否為關鍵。指令碼會依照列出的順序執行。

這些指令碼包括下列各項：

  - ClientVersionFilter 會提供系統管理員用來指定集區所支援之用戶端版本的方法。用戶端版本篩選器會檢查用戶端版本，然後可能會阻止用戶端登入，或者對使用者顯示訊息，指出其正在使用不支援的用戶端。用戶端版本篩選器也可以設定為對使用者顯示包含最新可下載用戶端版本之 URL 的訊息。

  - TranslationService 會根據系統管理員所定義的正規化規則，將使用者所撥的號碼轉譯為 E.164 號碼。如需詳細資訊，請參閱 [Lync Server 2013 中的轉譯規則](lync-server-2013-translation-rules.md)。

  - IncomingFederation 強制對租用戶之間和外部部署之傳入訊息進行租用戶層級同盟驗證。

  - UserServices 是前端伺服器的 SIP 登錄器、目前狀態和會議元件。它可為建置在 SIP Proxy 上方的 IM、目前狀態及會議功能提供緊密的整合。

  - InterClusterRouting 負責將通話路由傳送至被呼叫者的主要登錄器集區。如需詳細資訊，請參閱 [Lync Server 2013 的前端伺服器 VoIP 元件](lync-server-2013-front-end-server-voip-components.md)。

  - IIMFilter (智慧型 IM 篩選器) 會封鎖包含可點選 URL 或嘗試啟動檔案傳輸的訊息。IIMFilter 也會代表伺服器檢查用戶端版本。IIMFilter 會影響使用 Lync Server 或 Communicator 啟動的檔案傳輸。根據預設，在連結的第一個字元前面加入底線字元會停用可點選的連結。系統管理員可以變更此行為，以便封鎖連結，如此一來，伺服器就會封鎖含有可點選 URL 或是嘗試啟動檔案傳輸的訊息，使其無法抵達預定的目的地。IIMFilter 會安裝在所有執行 Lync Server 的伺服器 上，但不會安裝在 Proxy 伺服器和封存伺服器上。

  - UserPinService 可用來驗證電話撥入式會議的使用者個人識別碼 (PIN)。

  - DefaultRouting 是執行 Lync Server 之伺服器的預設路由應用程式。預設會加以啟用。路由應用程式會安裝在所有 Standard Edition 和 Enterprise Edition 伺服器上。

  - ExumRouting 會將通話路由傳送至 Exchange Server Unified Messaging (UM)。ExumRouting 會在有新的語音信箱訊息要處理時，決定適合將通話路由傳送至其中的 Exchange UM 伺服器。ExumRouting 也會處理其他 Exchange UM 整合方面，包括路由傳送至自動語音應答和訂戶存取。

  - OutboundRouting 會根據所撥的電話號碼與使用者的撥號授權，決定將通話路由傳送至電話號碼的閘道。如果閘道無法處理通話，OutboundRouting 也會一併處理通話的重新路由。

  - QoEAgent 會經由 SIP SERVICE 要求從端點接收經驗品質 (QoE) 資料報告，並且使用 HTTP POST 將資料傳送至監控伺服器上的目的地佇列或協力廠商取用者。如需詳細資訊，請參閱 [在 Lync Server 2013 中部署監控](lync-server-2013-deploying-monitoring.md)。

  - OutgoingFederation 強制對傳送至目標外部部署的訊息進行租用戶層級同盟驗證。

  - AcpRouting 將要送往音訊會議提供者的 INVITE 要求 Proxy 至音訊會議提供者閘道。

在 Edge Server 上執行的指令碼包括下列項目：

  - IIMFilter

  - 如果要求是送往目前的伺服器，則 OptionsHandler 會對傳入的 OPTIONS 要求回應 **200 OK** 。這用於拓撲驗證。

## 請參閱

#### 工作

[啟用或停用 Microsoft SIP Processing Language (MSPL) 伺服器應用程式](lync-server-2013-enable-or-disable-a-microsoft-sip-processing-language-mspl-server-application.md)  
[將 Microsoft SIP Processing Language (MSPL) 應用程式標示為 \[關鍵\] 或](lync-server-2013-mark-a-microsoft-sip-processing-language-mspl-application-as-critical-or-not-critical.md)

