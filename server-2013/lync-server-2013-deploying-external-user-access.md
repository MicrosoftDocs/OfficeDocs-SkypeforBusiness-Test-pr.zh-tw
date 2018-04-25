---
title: Lync Server 2013：部署外部使用者存取
TOCTitle: 部署外部使用者存取
ms:assetid: d40c9574-c16b-4fe6-b848-21ae0b7e4f0e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398918(v=OCS.15)
ms:contentKeyID: 49292433
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中部署外部使用者存取

 

_**上次修改主題的時間：** 2013-09-23_

若為 Microsoft Lync Server 2013 部署 Edge 元件，便可讓未登入您組織內部網路的外部使用者 (包括已驗證和匿名的遠端使用者、同盟協力廠商 (包括 XMPP 合作夥伴)、行動用戶端，以及公用立即訊息 (IM) 服務的使用者)，使用 Lync Server 與您組織中的其他使用者進行通訊。 Lync Server 2013 的部署和設定程序與 Lync Server 2010 有明顯差異。安裝和管理的工具與 Lync Server 2010 幾乎相同。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>安裝和設定 Microsoft Lync Server 2013Edge Server 的程序很複雜，可能需要投入大量心力進行規劃並與內部小組協調，包括 (但不限於) 安全性、網路、防火牆、網域名稱系統 (DNS)、負載平衡器及公開金鑰基礎結構 (PKI) 考量。建議您先檢閱和使用提供的規劃程序與文件後，再部署外部存取元件。此舉有助於減少在您進行部署程序時不希望的變更與問題發生的次數與頻率。如需規劃外部使用者存取方式的詳細資訊，請參閱＜ <a href="lync-server-2013-planning-for-external-user-access.md">在 Lync Server 2013 中規劃外部使用者存取</a>＞。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [Lync Server 2013 中外部使用者存取的部署檢查表](lync-server-2013-deployment-checklist-for-external-user-access.md)

  - [外部使用者為 Lync Server 2013 存取元件的系統需求](lync-server-2013-system-requirements-for-external-user-access-components.md)

  - [在周邊網路中準備安裝 Lync Server 2013 的伺服器](lync-server-2013-preparing-for-installation-of-servers-in-the-perimeter-network.md)

  - [在 Lync Server 2013 中建置 Edge 和 Director 拓撲](lync-server-2013-building-an-edge-and-director-topology.md)

  - [在 Lync Server 2013 中設定 Director](lync-server-2013-setting-up-the-director.md) (選用)

  - [在 Lync Server 2013 中設定 Edge Server](lync-server-2013-setting-up-edge-servers.md)

  - [設定 Lync Server 2013 的反向 Proxy 伺服器](lync-server-2013-setting-up-reverse-proxy-servers.md)

  - [在 Lync Server 2013 中設定外部使用者存取支援](lync-server-2013-configuring-support-for-external-user-access.md)

  - [Lync Server 2013 的 Lync-Skype 連線佈建指南](lync-server-2013-provisioning-guide-for-lync-skype-connectivity.md)

  - [在 Lync Server 2013 中設定 SIP 同盟、XMPP 同盟及 Public Instant Messaging](lync-server-2013-configuring-sip-federation-xmpp-federation-and-public-instant-messaging.md)

  - [在 Lync Server 2013 中部署行動性](lync-server-2013-deploying-mobility.md)

  - [在 Lync Server 2013 中驗證 Edge 部署](lync-server-2013-verifying-your-edge-deployment.md)

