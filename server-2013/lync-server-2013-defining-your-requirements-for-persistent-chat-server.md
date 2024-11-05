﻿---
title: Lync Server 2013：定義常設聊天室伺服器需求
TOCTitle: 定義組織的常設聊天室伺服器需求
ms:assetid: 568674fb-c08a-4170-ac38-e2f8428c69e0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398372(v=OCS.15)
ms:contentKeyID: 49290960
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中定義組織的常設聊天室伺服器需求

 

_**上次修改主題的時間：** 2014-01-15_

為組織部署 常設聊天室伺服器 之前，請務必考量下列關鍵問題以將部署最佳化：

  - 應該針對 常設聊天室伺服器 啟用哪些人員 (使用者設定檔)？ 常設聊天室伺服器 是透過全域、網站、集區或使用者層級上所設定的原則來啟用。

  - 應該針對 常設聊天室伺服器 啟用多少位使用者 (範圍)？ 常設聊天室伺服器 支援 150,000 位佈建的使用者 (透過原則來啟用)，以及最多 80,000 位同時使用 常設聊天室伺服器 的使用者。單一 常設聊天室伺服器 可支援 20,000 位連線的使用者，而單一 Persistent Chat Server 集區最多可以包含 4 部作用中伺服器，讓總共 80,000 位使用者可同時連線。

  - 您是從舊版 群組聊天伺服器移轉，還是首次部署 常設聊天室伺服器？

  - 是否有規範需求？ 常設聊天室伺服器 支援規範。相對於舊版 群組聊天伺服器部署中的個別電腦需求，Compliance Service 會在 常設聊天室伺服器前端伺服器 上組合執行。規範是選用的，如果選擇，就需要有規範資料庫，且必須將該資料庫設定為儲存規範資料和事件。您可能想要設定配置器，以便從規範資料庫中取得資料，並轉換為其他格式 (例如，XML 檔案，或 Exchange 裝載的封存)。

  - 您想要如何控制範圍、道德界限及存取？您可以定義 **\[類別\]** 來隔離這些界限，並選擇允許進入聊天室的人員，這些聊天室是建立於每個類別中。

  - 您想要如何控制可以建立聊天室的人員？您可以設定適用於類別的 **\[建立者\]**，讓這類人員可以建立聊天室。建立者可以根據類別所設定的 **\[允許的成員/遭拒的成員\]** 範圍，將其他成員指派為 **\[聊天室管理員\]**，以便持續不斷地管理聊天室 (新增或移除其他成員)。

  - 您想要如何建立聊天室？ 常設聊天室伺服器 提供一個 Web 型功能來建立和管理聊天室。此功能可以從 Lync 2013 用戶端啟動。您可以選擇定義自訂解決方案 (藉由使用 常設聊天室伺服器 軟體開發套件(SDK))，以實作您的業務需求和工作流程，並設定 常設聊天室伺服器，將使用者引導到您自訂的解決方案。

  - 您想要佈建哪些種類的增益集？ **\[增益集\]** 可以透過在 Lync 2013 用戶端中運用擴充性窗格來提供與聊天室相關的內容，藉以增強在聊天室中的使用體驗。您可以選擇哪些一般增益集最有用 (例如，貴公司的網站、內部共同作業元件等)。聊天室管理員可以選擇其中一個登錄的增益集，並視需要將它關聯至他們的聊天室。

  - 您有哪些種類的高可用性與災害復原需求？ 常設聊天室伺服器 支援 SQL Server 鏡像和 SQL Server 叢集，以提供高可用性，並在附有 SQL Server 記錄功能的延伸集區中，支援最多 8 部伺服器 (4 部作用中伺服器及 4 部待命伺服器)，以提供災害復原功能。

  - 是否有法規需求？如果您公司所在的國家/地區要求資料須保留在國內，您可能需要部署多個 Persistent Chat Server 集區，每個都位於指定的地理區域。聊天室、類別或增益集都不能跨越集區， 僅能屬於一個 Persistent Chat Server 集區。您可以為每個 Persistent Chat Server 集區 管理一組類別、增益集和聊天室。您可以設定使用者，使其能使用 AllowedMembers 範圍或聊天室的成員資格範圍類別 (根據您設計類別的方式而定)，存取一或多個集區中的聊天室。
    
    > [!IMPORTANT]  
    > 擁有多個 Persistent Chat Server 集區 不會為您提供更大的範圍 (在您的所有 Persistent Chat Server 集區上，仍然只有 80,000 位使用者可以同時連線)。支援多個 Persistent Chat Server 集區 的主要原因是要支持法規考量。
    
