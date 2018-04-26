---
title: Lync Server 2013 拓撲變更
TOCTitle: 拓撲變更
ms:assetid: 9e40ef93-9ab0-498c-9bbf-f94584353e53
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688153(v=OCS.15)
ms:contentKeyID: 49890229
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的拓撲變更

 

_**上次修改主題的時間：** 2012-10-02_

Lync Server 2013 的拓撲需求和考量與舊版不同，本節有相關說明。

## 新的前端集區架構

在 Lync Server 2013 中， Enterprise Edition前端集區的架構已變更為分散式系統架構。

有了這個新架構，後端資料庫不再是集區中的即時資料存放區。特定使用者的相關資訊會保存在集區中的三部前端伺服器。就每個使用者而言，一部前端伺服器會擔任該使用者資訊的主要伺服器，其餘兩部前端伺服器則擔任複本伺服器。如果其中某部前端伺服器停機，另一部擔任複本伺服器的前端伺服器就會自動遞補為主要伺服器。

此程序會在幕後進行，系統管理員不需要知道哪些前端伺服器是哪些使用者的主要伺服器。這樣的資料儲存區分佈可以提高集區內的效能和延展性，並且消除單一 後端伺服器產生的單一失敗點。

後端伺服器會擔任使用者與會議資料的備份儲存區，而且也會擔任「回應群組」資料庫等其他資料庫的主要儲存區。

這些改善也表示您規劃和維護集區的方式有所變更。建議您所有的 Enterprise Edition前端集區都包含至少三部前端伺服器，以提供 前端集區架構原本設計的完整數量的複本伺服器。此外，您在新增伺服器至 前端集區、從中移除伺服器或升級伺服器時，必須遵循特定程序。如需詳細資訊，請參閱＜ [Lync Server 2013 中的前端伺服器、立即訊息及顯示狀態的拓撲和元件](lync-server-2013-topologies-and-components-for-front-end-servers-instant-messaging-and-presence.md)＞。

## 伺服器角色拓撲變更

先前分開在不同伺服器上執行的某些伺服器角色，現在已合併成前端伺服器角色，讓您節省硬體成本

  - 在 Lync Server 2013 中，A/V 會議伺服器一律與前端伺服器位於同一部伺服器上。

  - 「監控」和「封存」的前端現在一律與前端伺服器位於同一部伺服器上。「監控」和「封存」仍然需要獨立的後端資料庫，這些後端資料庫可以與前端集區的後端資料庫位於同一部伺服器，也可以裝載於獨立的後端伺服器。

  - 常設聊天室伺服器 現在是伺服器角色。在 Microsoft Lync Server 2010 中， 群組聊天伺服器是 Microsoft Lync Server 2010 信任的第三方應用程式。在 Lync Server 2013 中， 常設聊天室伺服器 功能是以三個新的伺服器角色來實作：
    
      - **PersistentChatService ：**當成前端角色實作的主要 常設聊天室伺服器 服務
    
      - **PersistentChatStore ：**後端伺服器角色
    
      - **PersistentChatComplianceStore ：** 常設聊天室規範專用的後端伺服器角色

