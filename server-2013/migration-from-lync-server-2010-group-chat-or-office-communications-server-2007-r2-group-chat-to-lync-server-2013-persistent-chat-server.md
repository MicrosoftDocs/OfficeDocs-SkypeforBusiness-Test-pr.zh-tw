---
title: 從 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2 群組聊天移轉至 Lync Server 2013 常設聊天室伺服器
TOCTitle: 從 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2 群組聊天移轉至 Lync Server 2013 常設聊天室伺服器
ms:assetid: 5b4d3db1-6eba-4932-b49c-f60bcf9488f9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615442(v=OCS.15)
ms:contentKeyID: 49291025
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 從 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2 群組聊天移轉至 Lync Server 2013 常設聊天室伺服器

 

_**上次修改主題的時間：** 2012-10-06_

本節中的主題將引導您從 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2群組聊天移轉至 Lync Server 2013常設聊天室伺服器 的流程。若要讓 Lync Server 2013常設聊天室伺服器 部署與 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2群組聊天部署共存，本指南中也涵蓋一些在此混合環境中作業的基本資訊。本指南主要著重於 常設聊天室伺服器 的資料移轉。對於從舊版 Lync Server 移轉至 Lync Server 2013 的使用者，請參閱＜ [從 Lync Server 2010 移轉到 Lync Server 2013](migration-from-lync-server-2010-to-lync-server-2013.md)＞及＜ [從 Office Communications Server 2007 R2 移轉至 Lync Server 2013](migration-from-office-communications-server-2007-r2-to-lync-server-2013.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題假設您已安裝 Lync Server 2013，並且與 Lync Server 2010 或 Office Communications Server 2007 R2 共存。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本指南說明完成每階段移轉所需的一般步驟，並不會說明每一種可能的舊式部署拓撲或是每一種可能的移轉情況。因此，視部署之不同，可能不需要執行所述的每項步驟，或是有可能會需要執行額外的步驟。本指南也同時提供驗證步驟的範例。提供這些驗證步驟有助於了解要查看哪些內容，以確認在進行移轉的過程中，每個階段都已順利完成。可以針對您特定的移轉程序來修改這些驗證步驟。</td>
</tr>
</tbody>
</table>


本指南所提供的資訊旨在升級現有部署，並不會說明如何變更現有拓撲。本指南不包括新功能的實作。當詳細的程序記載於他處時，本指南將會引導您移至適當的文件或文件章節。

本文件定義下表所列之詞彙。

  - *移轉*   
    將您的部署從舊版 常設聊天室伺服器 (舊稱為 群組聊天伺服器) 移到 Lync Server 2013常設聊天室伺服器。

<!-- end list -->

  - *升級*   
    在伺服器上或在用戶端電腦上安裝較新版的軟體。

<!-- end list -->

  - *共存*   
    移轉期間所存在的暫時環境，某些功能會已移轉至 Lync Server 2013常設聊天室伺服器，而其他功能則仍停留在舊版 群組聊天伺服器中。

常設聊天室伺服器 是 Lync Server 2013 基礎結構的延伸模組。視您的拓撲而定，您可以將 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2群組聊天移轉至 Lync Server 2013常設聊天室伺服器。如需有關可用拓撲以及移轉 群組聊天伺服器之技術和軟體需求的詳細資訊，請參閱規劃文件中的 [在 Lync Server 2013 中規劃常設聊天室伺服器](lync-server-2013-planning-for-persistent-chat-server.md)。

如組織需要規範支援，現在會隨每部 常設聊天室伺服器 自動安裝。不再需要個別的規範伺服器。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>常設聊天室伺服器 必須安裝在 NTFS 檔案系統上，以強制檔案系統安全性。 常設聊天室伺服器 不支援 FAT32 檔案系統。<br />
如組織需要規範支援，現在會隨每部 常設聊天室伺服器 自動安裝。不再需要個別的規範伺服器。如需有關 Lync Server 2013常設聊天室伺服器 中變更的詳細資訊，請參閱＜入門＞文件中的 <a href="lync-server-2013-new-persistent-chat-server-features.md">Lync Server 2013 中的新常設聊天室伺服器功能</a>。</td>
</tr>
</tbody>
</table>


## 本節內容

  - [標準移轉案例 - 高層級](standard-migration-scenario-high-level.md)

  - [移轉程序 - 詳細資料](migration-process-details.md)

  - [共存考量](coexistence-considerations.md)

