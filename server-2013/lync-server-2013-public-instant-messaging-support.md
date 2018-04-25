---
title: Lync Server 2013：Public Instant Messaging 支援
TOCTitle: Public Instant Messaging 支援
ms:assetid: 1f45163b-52c6-4a78-b9c8-dfe3abe4e5eb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204732(v=OCS.15)
ms:contentKeyID: 49290301
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Public Instant Messaging 支援

 

_**上次修改主題的時間：** 2013-10-07_

Lync Server 2013 可支援使用授權的公用立即訊息 (IM) 連線供應商，以及使用可延伸訊息和顯示狀態通訊協定 (XMPP) 來實作特殊類型的同盟，其中可使用 Lync 2013 用戶端，啟用 Lync Server 以存取設定好的 XMPP 網域協力廠商。

## 公用 IM 連線供應商支援

目前支援的公用立即訊息連線協力廠商包括：

  - America Online

  - Windows Live

  - Yahoo\!

針對與 Windows Live 使用者通訊方面， Lync Server 2013 可支援對等 IM 以及音訊和視訊撥號。針對與 AOL 和 Yahoo\! 通訊方面， Lync Server 2013 可支援對等 IM，但可能需要個別的授權。

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
<td><ul>
<li><p>自 2012 年 9 月 1 日起，Microsoft Lync 公用 IM 連線使用者訂閱授權 (&quot;PIC USL&quot;) 無法再以新合約或續約的方式購買。持有使用中授權的客戶將可繼續與 Yahoo! Messenger 維持同盟關係直至服務終止日。目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的結束日期。如需詳細資訊，請參閱 <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>。</p></li>
<li><p>PIC USL 是針對每位使用者的每月訂閱授權，為 Lync Server 或 Office Communications Server 與 Yahoo! Messenger 同盟的必要授權。Microsoft 是否提供此項服務視 Yahoo! 的支援而定，而此基礎合約將告結束。</p></li>
<li><p>更勝以往，Lync 成為連接全世界組織之間以及個人之間的強大工具。除了 Lync Standard CAL 之外，與 Windows Live Messenger 同盟不需要其他使用者/裝置授權。此清單更將加入 Skype 同盟，讓 Lync 使用者可透過 IM 和語音觸及數億位使用者。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## XMPP 同盟支援

XMPP 同盟可支援 Lync 使用者和設定好的 XMPP 網域使用者 (其使用 GTalk 之類的公用供應商) 進行通訊。這些使用者可進行的通訊包括以下：

  - 對等 IM 和目前狀態

  - 在 Lync 用戶端中建立 XMPP 同盟連絡人

