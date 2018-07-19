---
title: 規劃 Lync Server 2013 中的可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟
TOCTitle: 規劃 Lync Server 2013 中的可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟
ms:assetid: 952b33e2-1f58-4831-9a39-1dfec2a316ad
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205107(v=OCS.15)
ms:contentKeyID: 49291701
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 規劃 Lync Server 2013 中的可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟

 

_**上次修改主題的時間：** 2012-10-22_

舊版的 Lync Server 和 Office Communications Server 提供可延伸傳訊和顯示狀態通訊協定 (XMPP) 閘道，此閘道可部署為個別的伺服器角色，以允許與 XMPP 部署進行同盟。在 Microsoft Lync Server 2013 中，XMPP 功能可以部署為一項功能。XMPP 功能會以兩個部分來安裝：在 Edge Server 上執行的 XMPP Proxy 以及在前端伺服器上執行的 XMPP 閘道。

XMPP 的部署與設定涵蓋於[在 Lync Server 2013 中部署外部使用者存取](lync-server-2013-deploying-external-user-access.md)中。您可以藉由在防火牆上定義連接埠和通訊協定規則、設定憑證及新增 DNS 記錄，來規劃在組織中支援 XMPP。本節中的下列主題摘要說明您為部署成功規劃 XMPP 同盟所需的資訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Microsoft 已測試過 Lync Server 2013 的 XMPP 功能，確定其可與 Google Talk 建立立即訊息同盟，而 Microsoft 也會負責這項功能的支援工作。對於其他 XMPP 系統，請連絡第三方廠商，確認其系統是否能與 Lync Server 2013 建立同盟，以及其是否有任何部署或疑難排解方面的建議。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [憑證摘要 - 可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟](lync-server-2013-certificate-summary-extensible-messaging-and-presence-protocol-xmpp-federation.md)

  - [連接埠摘要 - 可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟](lync-server-2013-port-summary-extensible-messaging-and-presence-protocol-xmpp-federation.md)

  - [DNS 摘要 - 可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟](lync-server-2013-dns-summary-extensible-messaging-and-presence-protocol-xmpp-federation.md)

## 請參閱

#### 工作

[在 Lync Server 2013 中設定 XMPP 同盟](lync-server-2013-setting-up-xmpp-federation.md)  
[在 Lync Server 2013 中設定原則以控制 XMPP 同盟使用者存取](lync-server-2013-configure-policies-to-control-xmpp-federated-user-access.md)  

#### 其他資源

[在 Lync Server 2013 中管理 XMPP 同盟夥伴](lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md)  
[Get-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsExternalAccessPolicy)  
[Get-CsXmppAllowedPartner](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsXmppAllowedPartner)  
[Get-CsXmppGatewayConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsXmppGatewayConfiguration)

