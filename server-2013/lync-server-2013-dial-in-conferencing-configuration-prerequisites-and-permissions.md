---
title: Lync Server 2013：電話撥入式會議組態先決條件和權限
TOCTitle: 電話撥入式會議組態先決條件和權限
ms:assetid: b3b251e5-78ac-44a2-8c36-2a061c9b2314
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412865(v=OCS.15)
ms:contentKeyID: 49292057
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的電話撥入式會議組態先決條件和權限

 

_**上次修改主題的時間：** 2012-06-20_

電話撥入式會議是 Lync Server 2013 會議工作量的選用元件。在設定電話撥入式會議之前需要安裝的元件，是在您使用 拓撲產生器設計拓撲，然後設定前端集區或 Standard Edition 伺服器時所部署。本主題描述在您可以設定電話撥入式會議之前，需要完成哪些作業。

本節假設您已閱讀規劃章節，這些章節與會議工作量和電話撥入式會議特別相關。

## 電話撥入式會議設定先決條件

電話撥入式會議需要下列 Lync Server 2013 元件：

  - 整合通訊應用程式服務 (UCAS) (稱為 *「應用程式服務」* )

  - 會議服務員應用程式

  - 會議宣告應用程式

  - 電話撥入式會議設定網頁

  - 至少一部 Lync Server 2013 中繼伺服器和一個 PSTN 閘道

您會在使用 拓撲產生器時部署這些元件，以定義並發行您的拓撲，然後部署前端集區或 Standard Edition 伺服器。如果您要部署 企業語音，應該在設定電話撥入式會議之前部署它。如果不要部署 企業語音，您可以在部署前端集區或 Standard Edition 伺服器之前，部署中繼伺服器和公用交換電話網路 (PSTN) 閘道。

> [!NOTE]  
> 如果您要從 Office Communications Server 2007 R2 升級至 Lync Server 2013，請在您計劃用來裝載 Lync Server 2013 會議的每個集區中部署電話撥入式會議。如需關於移轉電話撥入式會議的詳細資訊，請參閱 <a href="migration-from-office-communications-server-2007-r2-to-lync-server-2013.md">從 Office Communications Server 2007 R2 移轉至 Lync Server 2013</a>。



本節假設您已執行下列作業：

  - 將最新的更新套用至您的 Office Communications Server 2007 R2 環境 (如果您要移轉至 Lync Server 2013)。

  - 已使用 拓撲產生器來設計及設定您的拓撲。指定會議工作量時，您已選取電話撥入式會議選項。如需關於定義拓撲的詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中定義和設定拓撲](lync-server-2013-defining-and-configuring-the-topology.md)。

  - 已發行您的拓撲，並設定前端集區或 Standard Edition 伺服器。如需發行拓撲及安裝 Lync Server 2013 的詳細資訊，請參閱部署文件中的 [部署 Lync Server 2013](lync-server-2013-deploying-lync-server.md)。
    
    > [!NOTE]  
    > 當您安裝已發行的拓撲時，電話撥入式會議設定網頁會當做 Web 服務的一部分，安裝在前端伺服器或 Standard Edition 伺服器上。
    
    
    > [!IMPORTANT]  
    > 在部署 Lync Server 2013 之後，如果您變更 拓撲產生器中的檔案存放區路徑，則需要重新啟動會議服務員和會議宣告服務應用程式，才能使用新的路徑。
    


  - 已部署 企業語音。如果您沒有部署 企業語音，您可能是在 Enterprise Edition 前端伺服器或 Standard Edition 伺服器上配置了中繼伺服器，或者您部署了獨立的中繼伺服器，以及 PSTN 閘道。如需部署 企業語音的詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中部署企業語音](lync-server-2013-deploying-enterprise-voice.md)。 如需安裝獨立中繼伺服器和 PSTN 閘道的詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中部署中繼伺服器並定義對等項目](lync-server-2013-deploying-mediation-servers-and-defining-peers.md)。

下列流程圖顯示在您可以設定電話撥入式會議之前必須執行的步驟，以及設定電話撥入式會議的執行步驟。

**部署電話撥入式會議**

![電話撥入式會議部署流程圖](images/Gg412865.fde8c246-b5ed-4323-a6e7-af1983a5ec86(OCS.15).jpg "電話撥入式會議部署流程圖")

## 電話撥入式會議權限

若要設定電話撥入式會議，您需要使用下列系統管理工具：

  - Lync Server 2013 控制台

  - Lync Server 管理命令介面

您可以使用這些系統管理工具來設定電話撥入式會議設定，以及電話撥入式會議所需的撥號對應表、原則和其他設定。

視工作而定，設定電話撥入式會議需要下列任何系統管理角色：

  - **CsVoiceAdministrator**   此系統管理員角色可以建立、設定及管理語音相關的設定和原則。

  - **CsUserAdministrator**   此系統管理員角色可為使用者啟用及停用 Lync Server，以及指派現有的原則給使用者，例如會議原則和 PIN 原則。

  - **CsAdministrator**   此系統管理員角色可以執行 CsVoiceAdministrator 和 CsUserAdministrator 的所有工作。

## 請參閱

#### 概念

[在 Lync Server 2013 中部署企業語音](lync-server-2013-deploying-enterprise-voice.md)

