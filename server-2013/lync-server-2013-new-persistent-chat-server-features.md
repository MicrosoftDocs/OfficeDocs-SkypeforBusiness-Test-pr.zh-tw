---
title: Lync Server 2013：新常設聊天室伺服器功能
TOCTitle: 新常設聊天室伺服器功能
ms:assetid: c3ec6f33-6261-4bf5-aa31-baa8ab2a87d8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412965(v=OCS.15)
ms:contentKeyID: 49292231
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的新常設聊天室伺服器功能

 

_**上次修改主題的時間：** 2012-10-29_

Lync Server 2013, 常設聊天室伺服器 可讓您參與長期持續的多方主題式交談。 常設聊天室伺服器 可協助貴組織達成以下目標：

  - 改進地理位置分散且跨部門之小組間的通訊

  - 擴大資訊傳達和參與範圍

  - 改進大組織的通訊

  - 緩和資訊超載的狀況

  - 改進資訊傳達方式

  - 加強重要知識和資訊的傳播

Lync Server 2013常設聊天室伺服器 不適用於 Microsoft Office 365，目前僅適用於內部部署 Lync 2013 客戶。

Lync 2013 將常設聊天室功能整合到 Lync 2013 用戶端中。因此，使用者可以在 Lync 2013 用戶端中一次存取到立即訊息/目前狀態、音訊/視訊、會議和常設聊天室。如需 Lync 2013 用戶端的詳細資訊，請參閱<http://go.microsoft.com/fwlink/p/?linkid=270877>。

本主題描述新版 Lync Server 2013常設聊天室伺服器 與舊版 Microsoft Lync Server 2010 群組聊天之間的功能差異，包括下列項目：

  - 提供在 Lync Server 控制台中進行管理的能力，移除 群組聊天管理工具

  - 移除 群組聊天設定工具，將 常設聊天室伺服器 的組態設定整合到拓撲產生器中

  - 從舊版 常設聊天室伺服器 輕鬆移轉和升級

  - 提供高可用性和災害復原解決方案

如需最新版 常設聊天室伺服器 的詳細資訊，請參閱下列資源：

  - 位於 <http://go.microsoft.com/fwlink/p/?linkid=270945> 的常設聊天室說明，其中詳細列出各項常設聊天室功能、其運作方式，以及如何在執行常設聊天室伺服器時使用這些功能。

  - 規劃文件中的 [在 Lync Server 2013 中規劃常設聊天室伺服器](lync-server-2013-planning-for-persistent-chat-server.md)、部署文件中的 [在 Lync Server 2013 中部署常設聊天室伺服器](lync-server-2013-deploying-persistent-chat-server.md)、移轉文件中的 [從 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2 群組聊天移轉至 Lync Server 2013 常設聊天室伺服器](migration-from-lync-server-2010-group-chat-or-office-communications-server-2007-r2-group-chat-to-lync-server-2013-persistent-chat-server.md)，以及作業文件中的 [管理 Lync Server 2013 常設聊天室伺服器](managing-lync-server-2013-persistent-chat-server.md)，所有這些文章都提供設定 常設聊天室伺服器 的指示。

  - 常設聊天室伺服器 Documentation.msi 檔 (Windows Installer 檔案) 能讓使用者存取有關 常設聊天室伺服器 的完整離線文件。

## 常設聊天室伺服器 的重要拓撲變更

下列 常設聊天室伺服器 高階變更包括：

常設聊天室伺服器 現在是伺服器角色。在 Microsoft Lync Server 2010 中， 群組聊天伺服器是 Microsoft Lync Server 2010 信任的第三方應用程式。您可以使用 拓撲產生器，將 常設聊天室新增至您的 Lync Server 2013 拓撲。而在 Lync Server 2013 中， 常設聊天室伺服器 功能是透過下列三個新的伺服器角色實現：

  - **PersistentChatService :** 這是 常設聊天室的前端角色。在 Standard Edition 部署中， 常設聊天室伺服器 服務角色就像任何其他 Lync Server 角色，是共置於由啟動載入器所部署的 Standard Edition Server 上。在 Enterprise Edition 部署中， 常設聊天室服務角色就像任何其他 Lync Server 角色，是由啟動載入器部署於獨立電腦上。

  - **PersistentChatStore ：**與 常設聊天室內容資料庫對應的後端伺服器，所有聊天內容都儲存於此處。

  - **PersistentChatComplianceStore ：**與 常設聊天室規範資料庫對應的後端伺服器角色，所有規範事件都儲存於此處。

這三個 常設聊天室伺服器 角色是選用的，由想擁有完整 常設聊天室伺服器 功能的客戶自行安裝。只有在您選擇部署 常設聊天室規範時，才需要 **PersistentChatComplianceStore** 角色。

**PersistentChatService** 角色執行兩項服務：

  - 常設聊天室服務

  - 常設聊天室規範服務

在每個 常設聊天室伺服器 上都執行這些服務，可在多伺服器的 Persistent Chat Server 集區中以高可用性提供這些服務。

此外，為了在 常設聊天室中支援檔案上傳和下載， 常設聊天室伺服器 包含 Web 服務。在過去，此項服務是共置於 常設聊天室伺服器前端伺服器上，且先決條件為需要安裝 Internet Information Services (IIS)。在 Lync Server 2013常設聊天室伺服器 中，檔案上傳/下載 Web 服務是共置於 Lync Server 2013前端伺服器上，因此 Internet Information Services (IIS) 不再是 常設聊天室伺服器 的先決條件。檔案上傳/下載 Web 服務在 Internet Information Services (IIS) 管理員中是以 **PersistentChat** 識別。

> [!IMPORTANT]  
> 只有當 Lync Server 2013前端伺服器是 Standard Edition前端伺服器時， <strong>PersistentChatService</strong> 角色才能在該 前端伺服器的同一部伺服器上執行。 <strong>PersistentChatService</strong> 角色不能在沒有 Lync Server 2013前端伺服器的情況下執行，且只能安裝在 Lync Server 2013 部署環境中。



常設聊天室伺服器 已移除查閱服務。在 Lync Server 2010 群組聊天中，查閱服務會在每部 群組聊天伺服器前端伺服器上執行，並會路由至其中一部通道伺服器。 Lync Server 2013 是透過連絡人物件使用路由，每個連絡人物件都代表一個 Persistent Chat Server 集區， Lync Server前端伺服器會使用連絡人物件來識別要將要求路由傳送到的適當 Persistent Chat Server 集區以及該集區中某部執行 常設聊天室伺服器 的電腦。

Lync Server 2013 也修改了規範服務：

  - 在 Lync Server 2010 中，規範服務只在獨立伺服器上執行 (未與其他服務共置)。規範服務現在會在所有 常設聊天室伺服器前端伺服器上跟 常設聊天室服務一起執行，因此可在多伺服器 Persistent Chat Server 集區中展現高可用性。您可以設定單一規範配置器，從規範資料庫擷取資料並匯入到其他系統 (XML 檔案、Exchange 裝載的封存等)。 常設聊天室伺服器 包含 XML 配置器。

  - 在每部 常設聊天室伺服器前端伺服器上由 常設聊天室服務和規範服務共用的訊息佇列 (也稱為 MSMQ)，現在是僅供這兩個服務共用的私用佇列。所有規範服務都會寫入至同一個規範後端資料庫，也會讀取該資料庫以便傳送資料到自己的配置器執行個體。規範後端伺服器是以新的後端伺服器角色代表。
    
    > [!IMPORTANT]  
    > 在舊版中，所有規範資料僅處理一次。這些資料可由各種 Lync Server 2013常設聊天室伺服器 電腦上執行之規範服務所叫用的任何配置器執行個體處理。在 常設聊天室伺服器 中，任何一個配置器執行個體都能處理這些資料。
    
    
    > [!NOTE]  
    > 如需關於安裝訊息佇列的詳細資訊，請參閱部署文件中的 <a href="lync-server-2013-install-operating-systems-and-prerequisite-software-on-servers.md">在伺服器上安裝 Lync Server 2013 的作業系統和必要軟體</a>。
    


在 Lync Server 2013 中，高可用性和災害復原都有改進功能：

  - 高可用性改進功能：使用 SQL Server 鏡像來提供資料中心內 (網站內) 常設聊天室伺服器 內容資料庫與 常設聊天室 規範資料庫的高可用性。

  - 災害復原改進功能： 常設聊天室伺服器 支援延伸的集區架構，可將單一 Persistent Chat Server 集區延伸為跨越兩個網站 (亦即，拓撲中有單一邏輯集區，但集區內的伺服器實際位置跨越兩個網站)。要進行跨網站災害復原時，會使用 SQL Server 記錄傳送。

如需高可用性和災害復原的詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中針對高可用性和災害復原設定常設聊天室伺服器](lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md)。

## 常設聊天室伺服器 的重要管理變更

Lync Server 2013 提供下列項目，簡化 常設聊天室伺服器 的管理工作：

  - 整合管理功能。 Lync Server 2013 採用 Lync 系統管理員早已熟悉的工具，讓管理 常設聊天室伺服器 的工作更加輕鬆。 常設聊天室伺服器 提供與 Lync Server 控制台整合的系統管理使用者介面操作，能夠解決舊版 群組聊天伺服器使用者介面的效能問題。此外， 常設聊天室伺服器 也有一組用於管理 常設聊天室伺服器 類別、 常設聊天室伺服器 聊天室 (包括刪除聊天室和清除過時內容) 和增益集的 Windows PowerShell Cmdlet。

  - 簡化系統管理模型。為解決以下重要的客戶需求， Lync Server 2013 變更並簡化了 常設聊天室伺服器 模型：
    
      - 移除範圍與類別的複雜巢狀階層。
    
      - 支援讓打算移轉至 常設聊天室伺服器 的目前 MindAlign 客戶定義拒絕清單和允許清單 (範圍)。

## 使用者角色與舊版 群組聊天伺服器有何不同？

Lync Server 2010 群組聊天有使用者系統管理員角色、聊天室系統管理員角色以及可管理增益集的 Lync Server 系統管理員角色。 常設聊天室伺服器 則僅提供 常設聊天室系統管理員角色 (類似其他 Lync Server 角色型存取控制 (RBAC) 角色)。屬於此 RBAC 角色成員的任何人都能管理聊天室、增益集和類別 (進而獲得這些類別的使用者存取權) 以及設定 Persistent Chat Server 集區。

## 聊天室類別與舊版 群組聊天伺服器有何不同？

聊天室類別不再能採巢狀結構，且不再能修改根類別。舊版 群組聊天伺服器 中使用的範圍現在由AllowedMembers/DeniedMembers 包下 (惟舊版中並不支援指定拒絕清單)。由於不再有巢狀類別，因此無法覆寫範圍。 Lync Server 2013 的 常設聊天室系統管理員可以建立和管理聊天室類別。在建立和管理聊天室類別時， 常設聊天室系統管理員可以設定具有存取權的主體 (Active Directory 群組/容器/使用者) 成為特定類別之聊天室的成員/建立者。 常設聊天室系統管理員也可以新增 DeniedMembers 至類別，這些項目會成為允許清單的明確排除項目。DeniedMembers 會覆寫 AllowedMembers 的項目。

## 聊天室屬性與舊版 群組聊天伺服器有何不同？

Lync Server 2013常設聊天室伺服器 有新的開放聊天室概念。所有的允許成員都能加入這類聊天室，而不需要有專屬成員資格。

已移除舊版 常設聊天室伺服器 中的下列聊天室屬性：

  - 主題：聊天室現在只有描述。

  - 建立新成員清單：在 常設聊天室伺服器 中，所有聊天室一開始的成員清單都是空白 (最多可等於 \[允許成員\] 的成員清單)。

  - 檔案上傳：可控制是否允許檔案上傳/下載，以前是每個聊天室的個別設定。現在只能在類別層級設定，並套用至該類別的所有聊天室。

  - 聊天歷程記錄：可控制是否啟用聊天歷程記錄，以前是每個聊天室的個別設定。現在只能在類別層級設定，並套用至該類別的所有聊天室。

  - 邀請：聊天室一律繼承類別的邀請設定，但可在個別聊天室關閉邀請。如果類別已設為關閉邀請，則聊天室無法開啟邀請。

## 原則與舊版 群組聊天伺服器有何不同？

常設聊天室伺服器 對 常設聊天室的使用者/集區/網站/全域層級啟用了新的 Lync 原則。在 Lync 2013 用戶端，只有已被原則啟用 常設聊天室的使用者，才能使用 常設聊天室環境 (直接啟用或透過集區/網站/全域設定)。

舊版 群組聊天伺服器未將任何原則整合至 Lync Server 原則中。在使用者和類別/聊天室層級，使用每個使用者的 \[可以上傳檔案\] 功能，可以將該使用者設為使用者系統管理員、聊天室系統管理員，或設定使用者上傳檔案的能力。 常設聊天室伺服器 \[檔案上傳\] 功能則僅適用於類別層級。

## 記錄

常設聊天室伺服器 和 System Center Operations Manager 的記錄功能已整合至 Lync Server 2013 追蹤記錄中。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中規劃常設聊天室伺服器](lync-server-2013-planning-for-persistent-chat-server.md)

