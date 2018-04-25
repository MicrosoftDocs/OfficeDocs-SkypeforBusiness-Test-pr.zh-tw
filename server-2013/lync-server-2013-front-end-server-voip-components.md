---
title: Lync Server 2013：前端伺服器 VoIP 元件
TOCTitle: 前端伺服器 VoIP 元件
ms:assetid: 310e81a7-da45-47d4-95d0-92837e386502
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425812(v=OCS.15)
ms:contentKeyID: 49290501
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的前端伺服器 VoIP 元件

 

_**上次修改主題的時間：** 2012-10-01_

位於 前端伺服器上的 VoIP 元件如下：

  - 轉譯服務

  - 輸入路由元件

  - 輸出路由元件

  - Exchange UM 路由元件

  - Intercluster 路由元件

  - [Lync Server 2013 中的中繼伺服器元件](lync-server-2013-mediation-server-component.md)

## 轉譯服務

「轉譯服務」是負責根據系統管理員定義的正規化規則，將撥打的號碼轉譯成 E.164 格式或其他格式的伺服器元件。如果您的組織使用私人編號系統或使用不支援 E.164 的閘道或 PBX，則「轉譯服務」可以轉譯為 E.164 以外的其他格式。

## 輸入路由元件

輸入路由元件會根據使用者在其 企業語音用戶端上所指定的喜好設定來大量處理來電。它也有助於代理人響鈴與同時響鈴 (若使用者已設定) 的使用。例如，使用者可指定未應答的電話是否要轉接，還是只記錄下來進行通知。如果啟用了來電轉接，使用者就可以指定未應答的電話是否應該轉接到另一個號碼，或是轉接到已設定要提供來電接聽的 Exchange UM 伺服器。根據預設，所有的 Standard Edition 伺服器和 前端伺服器上都會安裝輸入路由元件。

## 輸出路由元件

輸出路由元件會將電話路由傳送到 PBX 或 PSTN 目的地。它會對來電者套用使用者的語音原則所定義的電話授權規則，然後決定最適合用來路由每通電話的 PSTN 閘道。根據預設，所有的 Standard Edition 伺服器和 前端伺服器上都會安裝輸出路由元件。

輸出路由元件所使用的路由邏輯會使用大的度量 (由網路或電話語音管理員根據其組織的需求而設定)。

## Exchange UM 路由元件

Exchange UM 路由元件會處理 Lync Server 和執行 Exchange 整合通訊 (UM) 之伺服器間的路由，以便整合 Lync Server 與 Unified Messaging 功能。

Exchange UM 路由元件也會在 Exchange UM 伺服器無法使用時，透過 PSTN 處理語音信箱的重新路由。如果您的分支網站有 企業語音使用者沒有可恢復的 WAN 連結來連到中央網站，您在分支網站部署的 Survivable Branch Appliance 將會在 WAN 中斷期間，繼續為分支網站使用者提供語音信箱功能。當 WAN 連結無法使用時， Survivable Branch Appliance 會執行下列動作：

  - 透過 PSTN，將未接聽的電話重新路由至中央網站的 Exchange Unified Messaging 伺服器

  - 提供使用者透過 PSTN 擷取語音信箱訊息的能力

  - 將未接來電通知排入佇列，然後在 WAN 連結恢復時將通知上傳至 Exchange UM 伺服器。

為了允許語音信箱重新路由，建議 Exchange 系統管理員應將 Exchange UM 自動語音應答 (AA) 設定成僅接受訊息。

如需這些功能的詳細資訊，請分別參閱＜ [在 Lync Server 2013 中規劃 Exchange Unified Messaging 整合](lync-server-2013-planning-for-exchange-unified-messaging-integration.md)＞及＜ [在 Lync Server 2013 中規劃企業語音復原](lync-server-2013-planning-for-enterprise-voice-resiliency.md)＞。

## Intercluster 路由元件

Intercluster 路由元件負責將電話路由至受話者的主要登錄器集區。如果該集區無法使用，此元件會轉而將電話路由至受話者的備份登錄器集區。如果無法透過 IP 網路聯繫到受話者的主要與備份登錄器集區，Intercluster 路由元件會透過 PSTN 將電話重新路由至使用者的電話號碼。

## VoIP 所需的其他前端伺服器元件

其他位於 前端伺服器或 Director 上而能提供 VoIP 必要支援，但本身不是 VoIP 元件的元件包括：

  - **使用者服務。**針對每一來電的目的地電話號碼執行反向號碼查閱，並將該號碼與目的地使用者的 SIP URI 相比對。使用這項資訊，「輸入路由元件」就可將電話分支到該使用者的註冊 SIP 端點。「使用者服務」是所有 前端伺服器和 Director 上的核心元件。

  - **使用者複寫器。**從 Active Directory 網域服務 擷取使用者電話號碼，並將其寫入 RTC 資料庫中的資料表，這些號碼在此資料庫中可供使用者服務和 Address Book Server 使用。「使用者複寫器」是所有 前端伺服器上的核心元件。

  - **Address Book Server。**將 Active Directory 網域服務 中的全域通訊清單資訊提供給 Lync Server 用戶端。也會擷取 RTC 資料庫中的使用者和連絡人資訊、將資訊寫入通訊錄檔案，然後將這些檔案儲存到共用資料夾，以供 Lync 用戶端下載。Address Book Server 會將資訊寫入 RTCAb 資料庫，而 通訊錄 Web 查詢服務會使用此資料庫來回應來自 Microsoft Lync 2010 Mobile 的使用者搜尋查詢。另外還可選用將寫入 RTC 資料庫的企業使用者電話號碼正規化，以便在 Lync 中佈建使用者連絡人。根據預設，所有的 前端伺服器都會安裝通訊錄服務。 通訊錄 Web 查詢服務依預設會隨 Web 服務一起安裝在每部 前端伺服器上。

