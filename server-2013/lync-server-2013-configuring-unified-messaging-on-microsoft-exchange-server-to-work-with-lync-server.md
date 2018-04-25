---
title: Lync Server 2013：設定 Microsoft Exchange Server 上的 Unified Messaging 以搭配 Lync Serve 使用
TOCTitle: 設定 Microsoft Exchange Server 上的 Unified Messaging 以搭配 Lync Server 2013 使用
ms:assetid: 058da9c4-23af-4ddb-9f63-70133a8aafc6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398106(v=OCS.15)
ms:contentKeyID: 49289964
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Microsoft Exchange Server 上的 Unified Messaging 以搭配 Lync Server 2013 使用

 

_**上次修改主題的時間：** 2012-10-11_

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您想使用 Exchange 整合通訊 (UM) 為 企業語音使用者提供來電接聽、Outlook Voice Access 或自動語音應答服務，請參閱規劃文件中的＜ <a href="lync-server-2013-planning-for-exchange-unified-messaging-integration.md">在 Lync Server 2013 中規劃 Exchange Unified Messaging 整合</a>＞，然後遵循本節中的指示執行作業。</td>
</tr>
</tbody>
</table>


若要設定 Exchange 整合通訊 (UM) 使用 企業語音，您需要執行下列工作：

  - 在執行 Exchange 整合通訊 (UM) 服務的伺服器上設定憑證
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>將所有 Client Access Server 和 Mailbox Server 新增至所有 UM SIP URI 撥號對應表。若未這麼做，撥出電話路由的運作將不如預期。</td>
    </tr>
    </tbody>
    </table>


  - 視需要建立一或多個 UM SIP URI 撥號對應表及訂戶存取電話號碼，然後建立對應的 Lync Server 撥號對應表。

  - 使用 **exchucutil.ps1** 指令碼：
    
      - 建立 UM IP 閘道。
    
      - 建立 UM 群組搜尋。
    
      - 授與 Lync Server 2013 權限以讀取 UM Active Directory 網域服務 物件。

  - 建立 UM 自動語音應答物件。

  - 建立訂戶存取物件。

  - 為每位使用者建立 SIP URI，並建立使用者與 UM SIP URI 撥號對應表的關聯。

## 需求和建議

在您開始之前，本節中的文件假設您已部署下列 Exchange 2013 角色：Client Access 和 Mailbox。在 Microsoft Exchange Server 2013 中， Exchange UM 會在這些伺服器上以服務來執行。

如需部署 Exchange 2013 的詳細資訊，請參閱 Exchange 2013 TechNet Library，網址為 [http://go.microsoft.com/fwlink/?linkid=266637\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=266637%26clcid=0x404)

也請注意以下事項：

  - 如果在多個樹系中安裝 Exchange UM，則必須針對每一個 UM 樹系執行 Exchange Server 整合步驟。此外，每個 UM 樹系都必須設定信任其中部署 Lync Server 2013 的樹系，而其中部署了 Lync Server 2013 的樹系都必須設定為信任每個 UM 樹系。

  - 執行 Unified Messaging 服務的 Exchange Server 角色及執行 Lync Server 2013 的伺服器都要執行整合步驟。您應該先執行 Exchange Server Unified Messaging 整合步驟，然後再執行 Lync Server 2013 整合步驟。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要了解哪些系統管理員角色在哪些伺服器上執行了哪些整合步驟，請參閱＜ <a href="lync-server-2013-deployment-process-for-integrating-on-premises-unified-messaging.md">整合內部部署 Unified Messaging 和 Lync Server 2013 的部署程序</a>＞。</td>
    </tr>
    </tbody>
    </table>


每部執行 Exchange UM 的伺服器上都必須提供下列工具：

  - Exchange 管理命令介面

  - 指令碼 **exchucutil.ps1**，它會執行下列工作：
    
      - 為每一個 Lync Server 2013 建立 UM IP 閘道。
    
      - 為每一個閘道建立群組搜尋。每一個群組搜尋的引導識別碼都會指定 UM SIP URI 撥號對應表，與閘道關聯之 前端集區或 Standard Edition 伺服器 會使用此對應表。
    
      - 授與 Lync Server 2013 權限以讀取 Active Directory 網域服務 中的 Exchange UM 物件。

## 本節內容

  - [在執行 Microsoft Exchange Server Unified Messaging 的伺服器上設定憑證](lync-server-2013-configure-certificates-on-the-server-running-microsoft-exchange-server-unified-messaging.md)

  - [針對 Lync Server 2013 在 Microsoft Exchange 上設定整合通訊](lync-server-2013-configure-unified-messaging-on-microsoft-exchange.md)

