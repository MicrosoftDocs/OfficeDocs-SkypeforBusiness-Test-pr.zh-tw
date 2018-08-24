---
title: Lync Server 2013：常設聊天室伺服器的元件和拓撲
TOCTitle: 常設聊天室伺服器的元件和拓撲
ms:assetid: 6a0a14a0-baad-44e9-b26e-4d192c0a0e70
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398500(v=OCS.15)
ms:contentKeyID: 49291206
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的常設聊天室伺服器的元件和拓撲

 

_**上次修改主題的時間：** 2012-10-05_

常設聊天室伺服器 支援單一伺服器及多伺服器設定。 常設聊天室伺服器 也可在 Lync Server 2013Standard Edition 伺服器上執行。這些設定包含下列 常設聊天室伺服器 元件及拓撲。

## 常設聊天室伺服器 元件

安裝最新版的 常設聊天室伺服器 需要下列元件：

  - 一或多部執行 常設聊天室伺服器 及提供下列服務的電腦：
    
      - 常設聊天室服務
    
      - 規範服務，會在啟用規範時開啟
    
    > [!IMPORTANT]  
    > 在 Lync Server 2013 中，用於檔案上傳/下載的 常設聊天室 Web 服務，現在與 Lync Server 2013前端伺服器組合。<br />
    > 聊天室管理的 常設聊天室 Web 服務也與 Lync Server 2013前端伺服器組合。


  - 伺服器 (使用鏡像時會有多部伺服器) 會裝載 SQL Server 後端資料庫，以裝載儲存聊天室內容、房間和類別的 常設聊天室內容資料庫。
    
    > [!NOTE]  
    > 後端資料庫可儲存交談記錄資料，包括類別和所建立 常設聊天室空間的相關資訊。
    


  - 如果啟用規範，伺服器 (使用鏡像時會有多部伺服器) 會裝載 SQL Server 後端資料庫，以裝載 常設聊天室規範資料庫，也就是基於法規遵循目的而儲存規範事件與交談內容的規範資料庫。

若要從個別電腦 (如管理主控台) 管理 常設聊天室伺服器，請使用電腦上的 Lync Server 控制台。而且，必須將此電腦部署至 Active Directory 網域服務 網域，且其樹系根中至少有一個通用類別目錄伺服器。

如需 常設聊天室伺服器 硬體和軟體需求的詳細資訊，請參閱支援文件中的 [Lync Server 2013 中常設聊天室伺服器的技術需求](lync-server-2013-technical-requirements-for-persistent-chat-server.md)、 [Lync Server 2013 的受支援硬體](lync-server-2013-supported-hardware.md)和 [Lync Server 2013 中的伺服器軟體和基礎結構支援](lync-server-2013-server-software-and-infrastructure-support.md)。

## 支援的組合

Lync Server 2013 支援各種組合案例，可在單一伺服器上執行多個元件 (如果您是小型組織) 或在不同伺服器上執行個別元件 (如果您是需要延展性和效能的大型組織)，藉此為您提供彈性以節省硬體成本。在您決定是否組合元件之前，務必考量延展性因素。

如果啟用規範，則 常設聊天室規範服務會與 Lync Server 2013前端伺服器組合。

常設聊天室伺服器 可部署於 Standard Edition 伺服器。 常設聊天室伺服器後端伺服器和 常設聊天室規範資料庫可與本機 SQL Server Express後端伺服器上的 Standard Edition 伺服器組合。如需可共同配置於該處之元件的詳細資訊，請參閱支援文件中的 [Lync Server 2013 中支援的伺服器組合](lync-server-2013-supported-server-collocation.md)。

對於 Lync Server 2013Enterprise Edition， 常設聊天室伺服器 無法在 Enterprise Edition Server 進行組合。 常設聊天室伺服器 的 SQL Server 資料庫可與 Enterprise Edition前端集區的 後端伺服器資料庫組合。 常設聊天室規範的 SQL Server 資料庫也可與 Enterprise Edition 集區的 後端伺服器資料庫組合。

> [!IMPORTANT]  
> 裝載 常設聊天室資料庫的伺服器也可裝載其他資料庫。不過，當您考慮將 常設聊天室資料庫與其他資料庫組合時，請留意您是否需儲存許多使用者的訊息， 常設聊天室資料庫所需的磁碟空間會大幅增加。基於此原因，我們建議不要將 常設聊天室資料庫與後端資料庫組合。



如果將 常設聊天室資料庫與後端資料庫組合，您可以針對任一或所有資料庫使用 SQL Server 的單一執行個體，也可以針對每個資料庫使用 SQL Server 的個別執行個體，但有以下限制：

  - SQL Server 的每個執行個體僅可包含一個單一後端資料庫和一個單一 常設聊天室資料庫。

如需有關所有伺服器角色和資料庫組合的詳細資訊，請參閱支援文件中的 [Lync Server 2013 中支援的伺服器組合](lync-server-2013-supported-server-collocation.md)。

## 常設聊天室伺服器 拓撲

常設聊天室伺服器 支援下列拓撲：

  - Lync Server 2013 Enterprise Edition 單一伺服器 常設聊天室伺服器前端伺服器

  - Lync Server 2013 Enterprise Edition 多伺服器 常設聊天室伺服器前端伺服器

  - 使用 SQL Server Express 的 Lync Server 2013Standard Edition 伺服器

  - Lync Server 2013Standard Edition 伺服器和 常設聊天室伺服器 位於個別伺服器上，並使用 Standard Edition 伺服器作為下一個躍點伺服器。

您可使用 拓撲產生器將 常設聊天室伺服器 新增至 Lync Server 2013 部署，也可以將單一伺服器或多伺服器 Persistent Chat Server 集區新增至拓撲。

> [!IMPORTANT]  
> 在您使用 拓撲產生器建立帶有單一伺服器的 Persistent Chat Server 集區後，就無法新增其他伺服器至集區。



## 單一伺服器拓撲

常設聊天室伺服器 的最基本組態和最簡單部署為單一 常設聊天室伺服器前端伺服器拓撲。此部署需要一部執行 常設聊天室伺服器 的伺服器 (如果已啟用規範，則可選擇性地執行 Compliance Service)、一部裝載這兩個 SQL Server 資料庫的伺服器，而且如果需要規範，則需要使用 SQL Server 資料庫來儲存規範資料。

> [!IMPORTANT]  
> Persistent Chat Server 集區若以單一伺服器部署在 拓撲產生器中啟動，您就無法新增其他伺服器。即使您正在使用單一伺服器，我們仍建議您使用多伺服器集區拓撲，這樣您就可以在日後視需要新增更多的伺服器。



下圖會針對含規範的單一 常設聊天室伺服器前端伺服器顯示拓撲的所有必要和選項元件。

**單一 Persistent Chat Server**

![安裝有 Compliance Service 的單一伺服器拓撲](images/Gg398500.9168fa52-61e0-4d17-a14d-45fd32e81456(OCS.15).jpg "安裝有 Compliance Service 的單一伺服器拓撲")

## 多部伺服器拓撲

若要提供較大的容量和可靠性，您可以部署多伺服器拓撲 (如 [在 Lync Server 2013 中規劃常設聊天室伺服器](lync-server-2013-planning-for-persistent-chat-server.md) 中所述)。多伺服器拓撲最多可以包含四部執行 常設聊天室伺服器 的作用中電腦 (高可用性和災害復原將允許最多八部，但只有四部可處於作用中狀態，其餘四部則為待命狀態)。每部伺服器支援最多 20,000 位使用者同時使用，總共 80,000 位使用者可以同時連線至含有 4 部伺服器的 Persistent Chat Server 集區。多伺服器拓撲與單一伺服器拓撲相同，差別在於有多部伺服器可裝載 常設聊天室伺服器，而且範圍更大。多部執行 常設聊天室伺服器 的電腦應該與 Lync Server 和 Compliance Service 位在相同的 Active Directory 網域服務 網域中。

下圖顯示多伺服器拓撲的所有元件，包括多部執行 常設聊天室伺服器 的電腦、選用的 Compliance Service 和獨立的規範資料庫。

**多部 Persistent Chat Server**

![多部伺服器拓撲](images/Gg398500.19aea898-28df-4d9b-903c-f72ef062d919(OCS.15).jpg "多部伺服器拓撲")

多伺服器拓撲提供伺服器功能的集區。在伺服器集區中， 常設聊天室服務會進行通訊和共用資料。例如， 原本張貼至某個 常設聊天室服務的交談記錄，可以由系統中的任何 常設聊天室服務取得。任何 常設聊天室服務都可以存取透過某個 常設聊天室服務上傳的檔案。使用者可連線至不同的 常設聊天室伺服器前端伺服器，並可互相交談及進行通訊。

TCP 8011 的預設連接埠會將伺服器連接至伺服器集區，並由 常設聊天室服務加以使用，以在伺服器間進行通訊或滿足管理需求。

