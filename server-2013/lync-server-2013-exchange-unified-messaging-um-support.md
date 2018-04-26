---
title: Lync Server 2013：Exchange Unified Messaging (UM) 支援
TOCTitle: Exchange Unified Messaging (UM) 支援
ms:assetid: 0da62b8d-7416-4fb8-a405-381ca805c53a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398179(v=OCS.15)
ms:contentKeyID: 49290087
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Exchange Unified Messaging (UM) 支援

 

_**上次修改主題的時間：** 2012-09-21_

Lync Server 2013 支援與 Exchange 整合通訊 (UM) 整合，以便將語音訊息和電子郵件訊息合併為單一訊息基礎結構。在 Exchange 2013 中， Exchange UM 包含 Exchange UM 服務 (在信箱伺服器上安裝並執行) 和 UM Call Router (在 Client Access Server 上安裝並執行)。針對 Lync Server 2013 Enterprise Voice 部署， Exchange UM 會將語音訊息和電子郵件訊息合併成可透過電話 (也就是，Outlook Voice Access) 或電腦來存取的單一存放區。 Exchange UM 與 Lync Server 2013 一起運作，可為 Enterprise Voice 的使用者提供來電接聽、Outlook Voice Access 和自動語音應答服務。

除了支援與 Exchange UM 的內部部署整合以外， Lync Server 2013 也支援與所裝載的 Exchange UM 整合。如果您將部分或所有的使用者移轉至裝載的 Exchange 服務提供者 (如 Microsoft Exchange Online)，這項支援可讓您提供語音訊息給使用者。

Lync Server 2013 支援下列版本：

  - Microsoft Exchange 2013

  - Microsoft Exchange Server 2010 (必要) 或最新的 Service Pack (建議)

  - Microsoft Exchange Server 2007 Service Pack 1 (SP1) (必要) 或最新的 Service Pack (建議)

您無法將 Exchange UM 與 Lync Server 2013 或 Lync Server 2013 資料庫組合在一起。您可以在個別的樹系中安裝 Exchange UM 和 Lync Server 2013。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>已部署 PBX 的 Enterprise Voice 部署可能不需要 Exchange UM，因為 PBX 可以繼續為所有使用者提供語音信箱和相關服務。如果您最後會撤銷 PBX (例如，如果您會針對公用交換電話網路 (PSTN) 連線部署 SIP 主幹)，則必須重新設定 Exchange UM，為先前使用 PBX 語音信箱系統的使用者提供語音信箱。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [Lync Server 2013 中內部部署 Unified Messaging 的元件和拓撲](lync-server-2013-components-and-topologies-for-on-premises-unified-messaging.md)

  - [Lync Server 2013 中的主控 Exchange UM 整合支援](lync-server-2013-support-for-hosted-exchange-um-integration.md)

