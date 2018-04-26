---
title: Lync Server 2013：建置 Edge 和 Director 拓撲
TOCTitle: 建置 Edge 和 Director 拓撲
ms:assetid: 11e5759e-d69f-4c39-8994-f467c279c558
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398202(v=OCS.15)
ms:contentKeyID: 49290138
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建置 Edge 和 Director 拓撲

 

_**上次修改主題的時間：** 2012-09-08_

建置拓撲牽涉到下列規劃與部署工作：

  - **規劃**   您需要為組織定義適當的拓撲，並識別部署所需的元件。以下是規劃程序中的標準步驟。 Microsoft Lync Server 2013 (隨附於 Lync Server 2013 的 規劃工具) 可方便您開始規劃程序，包括在需求與計劃都定案之後輕鬆加以變更。

  - **部署**   您透過 拓撲產生器定義的拓撲，對於任何 Lync Server 2013 伺服器的部署作業都非常重要。如果您未在規劃期間使用 拓撲產生器完成拓撲的定義與發行，在您部署 Edge Server 之前，必須先將它完成，並發行拓撲。

您至少需要部署一個內部集區才能部署 Edge Server 元件，而且您必須安裝 拓撲產生器以便部署內部集區。本節並未說明 拓撲產生器的安裝，因為該部分是內部集區的安裝程序。

如需這類集區的詳細資訊，請參閱＜ [Lync Server 2013 中外部使用者存取的部署檢查表](lync-server-2013-deployment-checklist-for-external-user-access.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您先前使用 拓撲產生器定義完整的拓撲，包括 Edge 拓撲，則您可以略過本節的＜ <a href="lync-server-2013-define-your-edge-topology.md">在 Lync Server 2013 中定義 Edge 拓撲</a>＞與＜ <a href="lync-server-2013-publish-your-topology.md">在 Lync Server 2013 中發行拓撲</a>＞工作，不過您還是需要完成＜ <a href="lync-server-2013-export-your-topology-and-copy-it-to-external-media-for-edge-installation.md">匯出 Lync Server 2013 拓撲並將拓撲複製到 Edge 安裝的外部媒體</a>＞工作。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [在 Lync Server 2013 中定義 Edge 拓撲](lync-server-2013-define-your-edge-topology.md)

  - [針對 Lync Server 2013 在拓撲中定義選用的 Director 拓撲](lync-server-2013-define-optional-director-topologies-in-your-topology.md)

  - [在 Lync Server 2013 中發行拓撲](lync-server-2013-publish-your-topology.md)

  - [匯出 Lync Server 2013 拓撲並將拓撲複製到 Edge 安裝的外部媒體](lync-server-2013-export-your-topology-and-copy-it-to-external-media-for-edge-installation.md)

