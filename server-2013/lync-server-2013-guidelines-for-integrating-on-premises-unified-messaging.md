---
title: Lync Server 2013：整合內部部署 Unified Messaging 的指導方針
TOCTitle: 整合內部部署 Unified Messaging 和 Lync Server 的指導方針
ms:assetid: 829ac017-6907-40f9-be22-787a28eae0ac
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398656(v=OCS.15)
ms:contentKeyID: 49291501
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 整合內部部署 Unified Messaging 和 Lync Server 2013 的指導方針

 

_**上次修改主題的時間：** 2012-09-25_

以下是部署 Enterprise Voice 時應納入考量的指導方針和最佳作法：

> [!IMPORTANT]  
> 只有在您也使用 UCMA 4 時， Exchange 整合通訊 (UM) 才支援 IPv6。



  - 部署 Lync Server 2013 Standard Edition Server 或 前端集區。如需安裝的詳細資訊，請參閱部署文件中的＜ [部署 Lync Server 2013](lync-server-2013-deploying-lync-server.md)＞。

  - 與 Exchange 系統管理員合作，確認每一個人將要執行的工作，以確保能夠順暢、成功地整合。

  - 在每個要為使用者啟用 Exchange UM 的 Exchange 整合通訊 (UM) 樹系中部署 Exchange Mailbox、Hub Transport、Client Access 及 Unified Messaging Server 角色。如需關於安裝 Exchange Server 角色的詳細資訊，請參閱 Microsoft Exchange Server 2013 文件。
    
    > [!IMPORTANT]  
    > 當 Exchange 整合通訊 (UM) 安裝完成時，其設定為使用自我簽署憑證。<br />
    > 但是，自我簽署憑證不會讓 Lync Server 2013 和 Exchange UM 互相信任，因此，這就是必須從這兩者都信任的憑證授權單位要求個別憑證的原因。


  - 如果 Lync Server 2013 和 Exchange UM 安裝在不同的樹系中，請將每一個 Exchange 樹系設定為信任 Lync Server 2013 樹系，以及將 Lync Server 2013 樹系設定為信任每個 Exchange 樹系。此外，請在 Lync Server 2013 樹系中的使用者物件上設定使用者的 Exchange UM 設定。這通常需要用到指令碼或 Identity Lifecycle Manager (ILM) 等跨樹系工具。

  - 必要時，安裝 Exchange 管理主控台以便管理 Unified Messaging 伺服器。

  - 取得 Outlook Voice Access 和自動語音應答的有效電話號碼。

  - 如果您使用的 Exchange UM 版本較 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 舊，請協調 Exchange UM SIP URI 撥號對應表和 Enterprise Voice 撥號對應表的名稱。

## 部署重複的 Exchange UM 伺服器

> [!IMPORTANT]  
> 建議您至少針對每個為組織設定的 Exchange UM SIP URI 撥號對應表部署兩部執行 Exchange UM 服務的伺服器。在提供擴充的容量之餘，部署重複的伺服器還能提供高可用性。伺服器發生故障時，您可以設定 Lync Server 2013 以容錯移轉至另一部伺服器。



以下範例設定可提供 Exchange UM 恢復能力。

**範例 1：Exchange UM 恢復能力**

![Exchange UM 範例 1](images/Gg398656.3644b847-0847-4550-a989-e3fc51de5c4b(OCS.15).jpg "Exchange UM 範例 1")

在範例 1 中，Tukwila 資料中心內的 Exchange UM 伺服器 1 和伺服器 2 均已啟用；Dublin 資料中心內的 Exchange UM 伺服器 3 和伺服器 4 均已啟用。當 Tukwila 中的 Exchange UM 停止運作時，應分別將伺服器 1 和 2 的網域名稱系統 (DNS) A 記錄設定為指向伺服器 3 和 4。當 Dublin 中的 Exchange UM 停止運作時，應分別將伺服器 3 和 4 的 DNS A 記錄設定為指向伺服器 1 和 2。

> [!Note]  
> 在範例 1 中，您還需要在每部 Exchange UM 伺服器上指派以下任一憑證：
> <ul>
> <li><p>在主體替代名稱 (SAN) 中使用含萬用字元的憑證。</p></li>
> <li><p>在 SAN 中分別放入每部 Exchange UM 伺服器的完整網域名稱 (FQDN)。</p></li></ul>


**範例 2：Exchange UM 恢復能力**

![Exchange UM 範例 2](images/Gg398656.15754273-306e-448d-b258-84bc2936a2e8(OCS.15).jpg "Exchange UM 範例 2")

在範例 2 中，於正常運作情況下，Tukwila 資料中心內的 Exchange UM 伺服器 1 和伺服器 2 均已啟用；Dublin 資料中心內的 Exchange UM 伺服器 3 和伺服器 4 均已啟用。這四部伺服器均包含在 Tukwila 使用者的 SIP URI 撥號對應表中，不過伺服器 3 和 4 均已停用。當 Tukwila 的 Exchange UM 伺服器發生如停止運作等的情況時，應停用 Exchange UM 伺服器 1 和 2 並啟用 Exchange UM 伺服器 3 和 4，以將 Tukwila Exchange UM 的流量路由傳送至 Dublin 的伺服器。

如需關於如何將 Exchange 2013 上的 Unified Messaging 啟用或停用的詳細資訊，請參閱「Integrate Exchange 2013 UM with Lync Server」(網址為 [http://go.microsoft.com/fwlink/?linkid=265372\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=265372%26clcid=0x404)，可能為英文網頁)。

如需如何在 Microsoft Exchange Server 2010 上啟用或停用 Unified Messaging 的詳細資訊，請參閱：

  - 「在 Exchange 2010 上啟用整合通訊」(網址為： [http://go.microsoft.com/fwlink/?linkid=204418\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=204418%26clcid=0x404))。

  - 「在 Exchange 2010 上停用整合通訊」(網址為： [http://go.microsoft.com/fwlink/?linkid=204416\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=204416%26clcid=0x404))。

## 請參閱

#### 概念

[整合內部部署 Unified Messaging 和 Lync Server 2013 的部署程序](lync-server-2013-deployment-process-for-integrating-on-premises-unified-messaging.md)

