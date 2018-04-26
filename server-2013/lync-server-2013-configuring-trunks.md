---
title: Lync Server 2013：設定主幹
TOCTitle: 設定主幹
ms:assetid: 0c339511-a185-484e-94f0-dbe918b7e48a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398170(v=OCS.15)
ms:contentKeyID: 49290067
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定主幹

 

_**上次修改主題的時間：** 2012-11-01_

在 企業語音部署中，您可以在中繼伺服器與下列其中一或多個對等 (Peer) 之間設定主幹，以便為您組織中的 企業語音用戶端和裝置提供公用交換電話網路 (PSTN) 連線能力：

  - 網際網路電話語音服務提供者 (ITSP) 的 SIP 主幹連線

  - PSTN 閘道

  - 專用交換機 (Private branch exchange，PBX)

如需詳細資訊，請參閱規劃文件中的＜ [在 Lync Server 2013 中規劃 PSTN 連線](lync-server-2013-planning-for-pstn-connectivity.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在您開始進行主幹設定之前，請確認已建立拓撲，而且中繼伺服器及其對等已設定好，並彼此產生關聯。如需詳細資訊，請參閱部署文件中的＜ <a href="lync-server-2013-define-a-gateway-in-topology-builder.md">在 Lync Server 2013 中於拓撲產生器內定義閘道</a>＞。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在主幹設定過程中，您可以啟用 Lync Server 2013 媒體旁路功能，讓媒體避開中繼伺服器。不論是否啟用媒體旁路功能，都可以設定主幹，但強烈建議您啟用該功能。如需詳細資訊，請參閱規劃文件中的＜ <a href="lync-server-2013-planning-for-media-bypass.md">在 Lync Server 2013 中規劃媒體旁路</a>＞。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [Lync Server 2013 中的多主幹支援](lync-server-2013-multiple-trunk-support.md)

  - [Lync Server 2013 中的主幹間路由](lync-server-2013-inter-trunk-routing.md)

  - [檢視 Lync Server 2013 中的主幹設定資訊](lync-server-2013-view-trunk-configuration-information.md)

  - [在 Lync Server 2013 中設定含媒體旁路的主幹](lync-server-2013-configure-a-trunk-with-media-bypass.md)

  - [在 Lync Server 2013 中設定無媒體旁路的主幹](lync-server-2013-configure-a-trunk-without-media-bypass.md)

  - [在 Lync Server 2013 中建立新的主幹組態設定集合](lync-server-2013-create-a-new-collection-of-trunk-configuration-settings.md)

  - [在 Lync Server 2013 中刪除現有的 SIP 主幹組態設定集合](lync-server-2013-delete-an-existing-collection-of-sip-trunk-configuration-settings.md)

  - [在 Lync Server 2013 中修改 SIP 主幹組態設定](lync-server-2013-modify-sip-trunk-configuration-settings.md)

  - [在 Lync Server 2013 中測試 SIP 主幹組態設定](lync-server-2013-test-sip-trunk-configuration-settings.md)

  - [檢視 Lync Server 2013 中個別 SIP 主幹的相關資訊](lync-server-2013-view-information-about-individual-sip-trunks.md)

## 請參閱

#### 工作

[在 Lync Server 2013 中於拓撲產生器內定義閘道](lync-server-2013-define-a-gateway-in-topology-builder.md)  

#### 其他資源

[在 Lync Server 2013 中規劃 PSTN 連線](lync-server-2013-planning-for-pstn-connectivity.md)  
[在 Lync Server 2013 中規劃媒體旁路](lync-server-2013-planning-for-media-bypass.md)

