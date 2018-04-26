---
title: Lync Server 2013：規劃外部使用者存取
TOCTitle: 規劃外部使用者存取
ms:assetid: ea098933-eff5-461e-aba3-e7f128784dc2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399048(v=OCS.15)
ms:contentKeyID: 49292691
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中規劃外部使用者存取

 

_**上次修改主題的時間：** 2013-01-19_

組織中多數通訊可能都包含非內部網路的服務與使用者。這些服務與使用者包括暫時或永久位於異地的員工、客戶或協力廠商組織的員工、使用公用立即訊息 (IM) 服務的人員，以及您邀請參加會議或簡報的潛在客戶、協力廠商及匿名使用者。在此文件中，這些人統稱為 *「外部使用者」* (External User)。

有了 Microsoft Lync Server 2013，您組織中的使用者就可以使用 IM 和目前狀態與外部使用者進行通訊，同時可以與異地員工和其他類型的外部使用者一起參與音訊/視訊 (A/V) 會議和 Web 會議。您也可以從行動裝置和透過 Enterprise Voice 支援外部存取。不屬於組織成員的外部使用者可利用匿名身份參與 Lync Server 2013 會議。

若要跨組織的防火牆支援通訊，您可以在周邊網路 (也稱為 DMZ、非軍事區和遮蔽式子網路) 中部署 Lync Server 2013 Edge Server。Edge Server 會控制防火牆外部的使用者能夠連線至內部 Lync Server 2013 部署的方式。另外還會控制與來自防火牆內部的外部使用者進行通訊。

根據您的需求而定，您可以在一個或多個位置部署一部或多部 Edge Server。本節描述 Lync Server 2013 中的外部使用者存取案例，並且解釋如何規劃您的邊緣與反向 Proxy 拓撲。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然您需要 Edge Server 才能支援 Enterprise Voice 和外部使用者存取，但是本節將著重於 IM、目前狀態、A/V 會議、同盟、Web 會議與 Lync Mobile 的支援。如需 Enterprise Voice 支援的詳細資訊，請參閱規劃文件中的＜ <a href="lync-server-2013-planning-for-enterprise-voice.md">在 Lync Server 2013 中規劃企業語音</a>＞。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [在 Lync Server 2013 中會影響 Edge Server 規劃的變更](lync-server-2013-changes-in-lync-server-that-affect-edge-server-planning.md)

  - [外部使用者為 Lync Server 2013 存取元件的系統需求](lync-server-2013-system-requirements-for-external-user-access-components.md)

  - [Lync Server 2013 中的外部使用者存取概觀](lync-server-2013-overview-of-external-user-access.md)

  - [了解自動探索](lync-server-2013-understanding-autodiscover.md)

  - [在 Lync Server 2013 中選擇拓撲](lync-server-2013-choosing-a-topology.md)

  - [Lync Server 2013 中的資料收集](lync-server-2013-data-collection.md)

  - [針對 Lync Server 2013 判定 DNS 需求](lync-server-2013-determine-dns-requirements.md)

  - [決定 Lync Server 2013 的外部 A/V 防火牆和連接埠需求](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md)

  - [在 Lync Server 2013 中規劃 Edge Server 憑證](lync-server-2013-plan-for-edge-server-certificates.md)

  - [Lync Server 2013 中的外部使用者存取案例](lync-server-2013-scenarios-for-external-user-access.md)

