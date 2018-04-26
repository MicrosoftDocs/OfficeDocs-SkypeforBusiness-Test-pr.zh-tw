---
title: Lync Server 2013：管理 Lync Server 災害復原、高可用性及備份服務
TOCTitle: 管理 Lync Server 2013 災害復原、高可用性及備份服務
ms:assetid: f4cd36fb-ffd6-48fa-b761-e11b3bcff91a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721939(v=OCS.15)
ms:contentKeyID: 49890509
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 管理 Lync Server 2013 災害復原、高可用性及備份服務

 

_**上次修改主題的時間：** 2012-11-12_

本節包含災難復原作業，以及維護同步處理配對前端集區資料的「備份服務」的程序。

容錯移轉與容錯回復均為手動的災難復原程序。如果發生災難，系統管理員系統管理員必須手動觸發容錯移轉程序。這同樣適用於集區配對後的容錯回復。

本節其餘的災難復原程序的假設前提如下：

  - 您已有位於不同網站的配對前端集區部署，如 [在 Lync Server 2013 中規劃高可用性和災害復原](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)所述；並已在這些配對集區中執行「備份服務」以保持同步處理。

  - 中央管理存放區 如果不是由配對集區中的任一個代管，則會同時在這兩個配對的集區中安裝並執行；其中一個集區代管作用中主資料庫，另一個集區代管待命資料庫。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在下列程序中， <em>PoolFQDN</em> 參數會參照受災難影響的集區 FQDN，而非造成重新導向受影響使用者的集區。對於同一組受影響的使用者而言，這是指容錯移轉與容錯回復 Cmdlet 中的同一個集區 (亦即容錯移轉前先成為使用者隸屬的集區)。<br />
例如，假設在某個案例中，所有隸屬於要位於集區 P1 的使用者均容錯移轉至容錯回復集區 P2；如果系統管理員想將目前由 P2 服務的所有使用者移為由 P1 服務，必須執行下列步驟：
<ol>
<li><p>使用容錯回復 Cmdlet，將所有原先主要在 P1 的使用者從 P2 容錯回復至 P1。在本案例中， <em>PoolFQDN</em> 是 P1 的 FQDN。</p></li>
<li><p>使用容錯移轉 Cmdlet，將所有原先主要在 P2 的使用者從 P1 容錯移轉至 P2。在本案例中， <em>PoolFQDN</em> 是 P2 的 FQDN。</p></li>
<li><p>如果系統管理員稍後想將那些 P2 使用者容錯回復至 P2，則 <em>PoolFQDN</em> 是 P2 的 FQDN。</p></li>
</ol>
請注意，必須在執行上述步驟 2 前先執行步驟 1，才能保留集區的完整性。如果在執行步驟 1 前先執行步驟 2，則步驟 2 的 Cmdlet 會失敗。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [在 Lync Server 2013 中設定和監控備份服務](lync-server-2013-configuring-and-monitoring-the-backup-service.md)

  - [在 Lync Server 2013 中容錯移轉集區](lync-server-2013-failing-over-a-pool.md)

  - [在 Lync Server 2013 中容錯回復集區](lync-server-2013-failing-back-a-pool.md)

  - [在 Lync Server 2013 中容錯移轉鏡像資料庫](lync-server-2013-failing-over-a-mirrored-database.md)

  - [在 Lync Server 2013 中容錯移轉用於 Lync Server 同盟的 Edge 集區](lync-server-2013-failing-over-the-edge-pool-used-for-lync-server-federation.md)

  - [在 Lync Server 2013 中容錯移轉用於 XMPP 同盟的 Edge 集區](lync-server-2013-failing-over-the-edge-pool-used-for-xmpp-federation.md)

  - [在 Lync Server 2013 中容錯回復 Lync Server 同盟或 XMPP 同盟使用的 Edge 集區](lync-server-2013-failing-back-the-edge-pool-used-for-lync-server-federation-or-xmpp-federation.md)

  - [在 Lync Server 2013 中變更與前端集區相關聯的 Edge 集區](lync-server-2013-changing-the-edge-pool-associated-with-a-front-end-pool.md)

  - [在 Lync Server 2013 中使用備份服務還原會議內容](lync-server-2013-restoring-conference-contents-using-the-backup-service.md)

## 請參閱

#### 概念

[在 Lync Server 2013 中規劃高可用性和災害復原](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)

