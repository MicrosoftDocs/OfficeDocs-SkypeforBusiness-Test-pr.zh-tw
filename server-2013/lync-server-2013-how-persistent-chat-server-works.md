---
title: Lync Server 2013 中的常設聊天室伺服器運作方式
TOCTitle: Lync Server 2013 中的常設聊天室伺服器運作方式
ms:assetid: 3d04e9a1-3f0c-458e-bcbe-d27c8c464276
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ683096(v=OCS.15)
ms:contentKeyID: 49890029
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的常設聊天室伺服器運作方式

 

_**上次修改主題的時間：** 2012-11-21_

Lync Server 2013常設聊天室伺服器 可讓您參與多方、主題性的長期持續交談。常設聊天室伺服器 可協助組織達成以下目的：

  - 改進地理位置分散且跨部門之小組間的通訊

  - 擴大資訊傳達和參與範圍

  - 改進大組織的通訊

  - 緩和資訊超載的狀況

  - 改進資訊傳達方式

  - 加強重要知識和資訊的傳播

您可以搭配 Lync Server 2013 部署 常設聊天室伺服器 作為選用角色。常設聊天室 服務執行於專用集區，並且 Persistent Chat Server 集區 依賴 Lync Server 集區路由訊息給它。 用戶端將使用 eXtensible Chat Communication Over SIP (XCCOS)。Lync Server前端伺服器會設定為將流量路由至 Persistent Chat Server 集區。

## 高層架構

下列圖表提供 常設聊天室伺服器 架構與服務的高層檢視。

**Persistent Chat Server 高層架構**

![Persistent Chat Server 架構。](images/JJ683096.5db6f36f-4461-4d87-ba77-463b7ffe609b(OCS.15).jpg "Persistent Chat Server 架構。")

**Persistent Chat Server 高層服務**

![Persistent Chat Server 元件。](images/JJ683096.b6d743aa-3a86-4081-aaef-4fe3257db4e7(OCS.15).jpg "Persistent Chat Server 元件。")

常設聊天室伺服器前端伺服器上執行兩個服務：

  - 常設聊天室 (通道)

  - 規範

## 常設聊天室 (通道) 服務

常設聊天室 (通道) 服務是負責 常設聊天室伺服器 的核心服務。此服務提供下列功能：

  - 接受傳入訊息

  - 登錄及列出 常設聊天室 聊天室內的線上參與者

  - 重新傳輸訊息給其他通道訂閱者

  - 實作通道管理、聊天室邀請、搜尋及新內容通知的邏輯

常設聊天室 (通道) 服務會使用常設聊天室存放區，儲存及存取聊天室內容與其他系統中繼資料 (授權規則等等)。此服務會將上傳至聊天室的檔案儲存於常設聊天室檔案存放區。

## 規範服務

規範服務是 常設聊天室伺服器 的選用元件，負責將聊天內容與事件封存至常設聊天室規範存放區。如果組織規定中要求封存常設聊天室活動，則可以部署選用的常設聊天室規範服務。規範服務會安裝在常設聊天室集區中的每個 常設聊天室伺服器 上。設定之後，常設聊天室伺服器 規範服務會記錄使用者活動，例如加入與離開聊天室，以及張貼與讀取訊息。規範服務會將需要封存的檔案儲存在常設聊天室規範檔案存放區。

## 常設聊天室 Web 服務

Lync Server前端伺服器上有兩個服務的執行依存於 Internet Information Services (IIS)，並實作為 Web 元件：

  - **用於檔案上傳/下載的常設聊天室 Web 服務** 負責從聊天室張貼及擷取檔案。

  - **用於聊天室管理的常設聊天室 Web 服務** 負責提供使用者管理聊天室以及建立新聊天室的功能。

## 如何開始使用 常設聊天室伺服器？

常設聊天室伺服器 是 Lync Server 2013 基礎結構內的選用伺服器角色。如果安裝了 常設聊天室伺服器 角色，則任何讓管理員透過原則啟用的使用者，都可以藉由 Lync 2013 用戶端來使用常設聊天室。如需如何部署 常設聊天室伺服器 以及如何透過原則讓使用者得以利用其功能的詳細資訊，請參閱＜[在 Lync Server 2013 中部署常設聊天室伺服器](lync-server-2013-deploying-persistent-chat-server.md)＞。

如需如何在 常設聊天室伺服器 部署上組態設定的詳細資訊，請參閱＜[在 Lync Server 2013 中部署常設聊天室伺服器](lync-server-2013-deploying-persistent-chat-server.md)＞及＜[管理 Lync Server 2013 常設聊天室伺服器](managing-lync-server-2013-persistent-chat-server.md)＞。

如需如何透過原則讓使用者得以在 Lync 2013 用戶端中利用常設聊天室功能的詳細資訊，請參閱＜[在 Lync Server 2013 中部署常設聊天室伺服器](lync-server-2013-deploying-persistent-chat-server.md)＞及＜[管理 Lync Server 2013 常設聊天室伺服器](managing-lync-server-2013-persistent-chat-server.md)＞。

如果部署常設聊天室規範，如需如何組態規範設定的詳細資訊，請參閱＜[管理 Lync Server 2013 常設聊天室伺服器](managing-lync-server-2013-persistent-chat-server.md)＞。

## 常設聊天室通話流程

Lync 用戶端使用 XCCOS 與常設聊天室服務進行通訊。下列順序描述登入程序、一般聊天室訂閱以及訊息張貼的情況。

## 登入

下列順序描述登入程序。

1.  Lync 用戶端先傳送 SIP SUBSCRIBE，以從伺服器擷取頻內佈建文件。此文件會指出常設聊天室是否針對使用者啟用或停用，以及 Persistent Chat Server 集區的 SIP URI 清單。

2.  Lync 用戶端傳送 SIP INVITE 訊息至 常設聊天室伺服器 的 SIP URI (從上一步驟取得)。INVITE 順序之後接著是 200 OK 和 ACK，現在 Lync 用戶端已經與 常設聊天室伺服器 端點開啟了 SIP 工作階段。於是，用戶端透過傳送 SIP INFO 訊息 (訊息中包含聊天訊息或要求伺服器採取行動的命令) 與 常設聊天室伺服器 進行通訊。所有這些訊息都會以 200 OK 或「503 服務無法使用」(亦即在伺服器負載過重的情況下) 進行認可。如果用戶端收到 503 回應，會重試訊息。(此範例未涵蓋 503 回應。) 如果伺服器接受訊息或命令，並傳送 200 OK，則會以個別 SIP INFO 訊息的形式提供用戶端回應。該回應會包含對原始命令的參考。

3.  Lync 用戶端傳送包含 XCCOS **getserverinfo** 命令的 SIP INFO 訊息。常設聊天室伺服器 以新的 SIP INFO 訊息回覆，其中包含有關常設聊天室服務組態的資訊。

4.  Lync 用戶端傳送包含 XCCOS **getassociations** 命令的 SIP INFO 訊息。常設聊天室伺服器 以新的 SIP INFO 訊息回覆，其中包含使用者為其成員的聊天室清單。Lync 用戶端重複該命令以擷取使用者為其管理員的聊天室清單。

5.  Lync 用戶端從「目前狀態」文件中取得追蹤聊天室的清單，其中每個追蹤聊天室是以 "roomSetting" 類別表示。所有追蹤聊天室會聯結包含 XCCOS **bjoin** 命令的單一 SIP INFO 訊息，命令中又包含聊天室 URI 的清單。因為追蹤聊天室的清單保存在伺服器上，在任何電腦上的任何用戶端對於指定的使用者 URI 都有同樣的追蹤聊天室清單。Lync 用戶端也會將開啟聊天室的清單保存在本機電腦登錄中 (如果使用者啟用此選項)，並且在登入時，對每個開啟聊天室傳送包含 XCCOS **join** 命令的 SIP INFO 訊息，以加入每個聊天室。因為此清單表保存在登錄中，在不同電腦上執行的兩個 Lync 用戶端可能會有不同的清單。

6.  對每個加入的聊天室，Lync 用戶端都會傳送包含 XCCOS **bccontext** 命令的 SIP INFO 訊息。常設聊天室伺服器 以新的 SIP INFO 訊息回覆，其中包含聊天室中最近的聊天訊息。

7.  Lync 用戶端傳送包含 XCCOS **getinv** (意指取得邀請) 命令的 SIP INFO 訊息，以對用戶端尚未見過的新聊天室要求邀請。常設聊天室伺服器 會以個別的 SIP INFO 訊息，傳回這些聊天室的清單。

## 訂閱聊天室及張貼訊息

下列順序描述一般聊天室訂閱及訊息張貼的情況。

1.  從 Lync 用戶端，使用者 1 按一下 **\[加入聊天室\]**、按一下 **\[搜尋\]**，然後輸入一些搜尋條件。用戶端傳送包含 XCCOS **chansrch** (聊天室搜尋) 命令以及搜尋條件的 SIP INFO 訊息。常設聊天室伺服器 查詢後端資料庫，然後以新的 SIP INFO 訊息回覆，其中包含符合搜尋條件的可用聊天室清單。

2.  使用者 1 選取要加入的聊天室，然後按一下 **\[追蹤此聊天室\]**。用戶端會對 常設聊天室伺服器 傳送 SIP INFO 訊息，其中包含 XCCOS **join** 命令以及使用者所選聊天室的聊天室識別碼。常設聊天室伺服器 以包含佈建資料的 SIP INFO 訊息回覆。

3.  Lync 用戶端對 常設聊天室伺服器 傳送包含 XCCOS **bccontext** (過期聊天內容) 命令的 SIP INFO 訊息。常設聊天室伺服器 擷取聊天記錄，然後以個別 SIP INFO 訊息傳回至用戶端。此時，使用者進入聊天室，準備就緒參與。

4.  使用者 1 輸入新訊息，然後按一下 **\[傳送\]**。Lync 用戶端以 SIP INFO XCCOS **grpchat** 命令，將訊息張貼到聊天室。常設聊天室伺服器 將此新訊息的複本儲存在常設聊天室後端資料庫。

5.  常設聊天室伺服器 傳送 SIP INFO XCCOS **grpchat** 訊息的個別複本給已進入聊天室的使用者 2。

## 常設聊天室規範通話流程

常設聊天室伺服器 使用訊息佇列 (亦稱為 MSMQ) 及額外的規範資料庫 (mgccomp) 來處理規範資料。下列事件順序描述如何處理訊息張貼事件，用以作為如何處理規範事件的範例。

1.  使用者在聊天室張貼訊息。

2.  常設聊天室伺服器 將與事件有關的資訊放置於私用「訊息佇列」佇列。

3.  常設聊天室 Compliance Server 從佇列讀取此事件，並且將它放置於 mgccomp 資料庫，以稍後處理。

4.  常設聊天室 Compliance Server 會定期處理資料庫中一組事件，並且將它們傳送到 常設聊天室 Compliance 配接器進行處理。

5.  如果配接器成功處理資料，常設聊天室 Compliance Server 會從 mgccomp 資料庫中刪除事件。

