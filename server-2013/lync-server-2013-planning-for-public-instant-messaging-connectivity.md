---
title: 規劃 Lync Server 2013 中的公用立即訊息連線
TOCTitle: 規劃 Lync Server 2013 中的公用立即訊息連線
ms:assetid: e75e8884-05c7-414a-8014-bc9aa8126fb7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205349(v=OCS.15)
ms:contentKeyID: 49292648
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 規劃 Lync Server 2013 中的公用立即訊息連線

 

_**上次修改主題的時間：** 2013-10-07_

Public Instant Messaging Connectivity 是一種同盟等級，此設定可讓您的內部及外部 Lync Server 2013 使用者從下列位置新增連絡人：

  - Messenger 連絡人

  - Yahoo\! 連絡人

  - America Online (AOL) 連絡人

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
<li><p>自 2012 年 9 月 1 日起，Microsoft Lync 公用 IM 連線使用者訂閱授權 (&quot;PIC USL&quot;) 無法再以新合約或續約的方式購買。持有使用中授權的客戶將可繼續與 Yahoo! Messenger 維持同盟關係直至服務終止日。目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的確切結束日期。如需詳細資訊，請參閱＜<a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>＞。</p></li>
<li><p>PIC USL 是針對每位使用者的每月訂閱授權，為 Lync Server 或 Office Communications Server 與 Yahoo! Messenger 同盟的必要授權。Microsoft 是否提供此項服務視 Yahoo! 的支援而定，而此基礎合約將不再續約。</p></li>
<li><p>更勝以往，Lync 成為連接全世界組織之間以及個人之間的強大工具。除了 Lync Standard CAL 之外，與 Windows Live Messenger 同盟不需要其他使用者/裝置授權。此清單更將加入 Skype 同盟，讓 Lync 使用者可透過 IM 和語音觸及數億位使用者。</p></li>
</ul></td>
</tr>
</tbody>
</table>


使用此同盟等級必須考量下列規劃：

  - Windows Live Messenger 使用者除了可與 Lync Server 2013 使用者互通立即訊息，還可以進行對等音訊/視訊通訊。您的 Edge Server 必須符合特定連接埠與通訊協定需求。如需詳細資訊，請參閱＜[決定 Lync Server 2013 的外部 A/V 防火牆和連接埠需求](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md)＞。

  - Yahoo 立即訊息除了平常在部署與規劃標準 Edge Server 所使用的需求外 (同盟提供)，並無特定需求。

  - America Online 要求指派到 Access Edge Service 的 Edge Server 憑證要有用戶端增強金鑰使用方法 (EKU)。

## 本章節內容

  - [憑證摘要 - Public Instant Messaging 連線](lync-server-2013-certificate-summary-public-instant-messaging-connectivity.md)

  - [連接埠摘要 - Public Instant Messaging 連線](lync-server-2013-port-summary-public-instant-messaging-connectivity.md)

  - [DNS 摘要 - Public Instant Messaging 連線](this-topic-is-no-longer-available.md)

