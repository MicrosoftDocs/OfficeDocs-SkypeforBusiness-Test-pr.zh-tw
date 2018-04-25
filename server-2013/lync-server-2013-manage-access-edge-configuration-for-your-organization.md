---
title: Lync Server 2013：管理組織的 Access Edge 設定
TOCTitle: 管理組織的 Access Edge 設定
ms:assetid: 0145eb08-984f-4ecd-bf9c-364817619c2a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ552443(v=OCS.15)
ms:contentKeyID: 49289892
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中管理組織的 Access Edge 設定

 

_**上次修改主題的時間：** 2012-11-01_

此為初稿文件，可能隨時變更。空白主題是內容的預留位置。

部署一或多部 Edge Server 之後，您必須透過組織支援的 Edge Server，啟用會議的外部網域或提供者存取、遠端使用者存取，以及匿名使用者存取類型。

下列選項包含可透過「Access Edge 設定」 頁面設定的存取類型：

  - **啟用同盟和公用 IM 連線**    如果您想支援使用者存取同盟協力廠商網域，請啟用這個選項。此設定會同時套用至「外部存取原則」 頁面上，針對全域、網站或使用者範圍設定的 SIP 同盟和 XMPP 同盟。若要套用同盟設定，您必須設定這兩個頁面的同盟支援。
    
    此外，還提供兩個選用設定選項：同盟協力廠商的探索方式，以及是否將封存免責聲明傳送給連絡人 (通知與您進行通訊的同盟連絡人，您的部署已啟用封存，因此將會封存通訊詳細資料)。
    
      - **啟用協力廠商網域探索**    選取這個選項可自動探索您可以同盟的網域。 Lync Server 2013 使用網域名稱系統 (DNS) 記錄嘗試探索未列在允許網域清單中的網域、自動評估來自探索之同盟協力廠商的傳入流量，以及根據信任層級、流量和管理員設定來限制或封鎖該流量。如果您未選取此選項，則只會針對包含在允許的網域清單中的網域使用者啟用同盟使用者存取。無論是否選取此選項，您都可以指定封鎖或允許個別網域，包括限制存取同盟網域中執行 Access Edge 服務的特定伺服器。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中針對允許的外部網域設定支援](lync-server-2013-configure-support-for-allowed-external-domains.md)＞。
    
      - **將封存免責聲明傳送給同盟協力廠商**    選取這個選項可將封存免責聲明訊息傳送給同盟協力廠商，通知協力廠商將會記錄通訊詳細資料。如果封存與同盟協力廠商網域的外部通訊，則應該啟用封存免責聲明通知，警告協力廠商您的部署將會封存其訊息及通訊詳細資料。如需封存的詳細資訊，請參閱＜ [在 Lync Server 2013 中定義封存需求](lync-server-2013-defining-your-requirements-for-archiving.md)＞。

  - **啟用遠端使用者存取**    如果您想要讓位於防火牆外部的組織內使用者 (例如在家工作與出差的使用者) 連線至 Lync Server，請啟用這個選項。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中啟用或停用遠端使用者存取](lync-server-2013-enable-or-disable-remote-user-access.md)＞。

  - **讓匿名使用者能夠存取會議**    如果您想讓內部使用者邀請外部匿名使用者加入其召開的會議，請啟用這個選項。啟用此設定只會允許匿名使用者加入會議。若要設定會議體驗和選項，以定義使用者可在會議中執行的工作及執行方式，並加入匿名使用者，請參閱＜ [建立或修改使用者站台或群組的會議使用者經驗](https://technet.microsoft.com/zh-tw/library/gg429715\(v=ocs.15\))＞及＜ [Lync Server 2013 中的會議原則設定參考](lync-server-2013-conferencing-policy-settings-reference.md)＞中的詳細資訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>除了啟用外部使用者存取支援，您還可以設定相關原則以控制組織遠端使用者存取，接著才將任何類型的外部使用者存取功能提供給使用者。如需建立、設定與套用外部使用者存取相關原則的詳細資訊，請參閱＜ <a href="lync-server-2013-manage-external-access-policy-for-your-organization.md">在 Lync Server 2013 中管理外部使用存取原則</a>＞。</td>
</tr>
</tbody>
</table>


**使用 Windows PowerShell Cmdlet 檢視 Access Edge 設定資訊**

  - 您可以使用 Windows PowerShell 和 **Get-CsAccessEdgeConfiguration** Cmdlet 檢視 Access Edge 設定資訊。此 Cmdlet 可從 Lync Server 2013 管理命令介面 或從 Windows PowerShell 的遠端工作階段執行。 如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。
    
    若要檢視所有 Access Edge 組態設定的資訊，請在 Lync Server 管理命令介面中輸入下列命令，然後按 ENTER 鍵：
    
        Get-CsAccessEdgeConfiguration
    
    這樣將傳回類似下列的資訊：
    
        Identity                               : Global
        AllowAnonymousUsers                    : False
        AllowFederatedUsers                    : False
        AllowOutsideUsers                      : True
        BeClearingHouse                        : False
        EnablePartnerDiscovery                 : False
        EnableArchivingDisclaimer              : False
        EnableUserReplicator                   : True
        KeepCrlsUpToDateForPeers               : True
        MarkSourceVerifiableOnOutgoingMessages : True
        OutgoingTlsCountForFederatedPartners   : 4
        DiscoveredPartnerStandardRate          : 20
        EnableDiscoveredPartnerContactsLimit   : True
        MaxContactsPerDiscoveredPartner        : 1000
        DiscoveredPartnerReportPeriodMinutes   : 60
        MaxAcceptedCertificatesStored          : 1000
        MaxRejectedCertificatesStored          : 500
        CertificatesDeletedPercentage          : 20
        RoutingMethod                          : UseDnsSrvRouting

## 本章節內容

  - [在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)

  - [在 Lync Server 2013 中啟用或停用探索同盟協力廠商](lync-server-2013-enable-or-disable-discovery-of-federation-partners.md)

  - [在 Lync Server 2013 中啟用或停用傳送封存免責聲明至同盟合作夥伴的功能](lync-server-2013-enable-or-disable-sending-an-archiving-disclaimer-to-federated-partners.md)

  - [在 Lync Server 2013 中啟用或停用遠端使用者存取](lync-server-2013-enable-or-disable-remote-user-access.md)

  - [在 Lync Server 2013 中啟用或停用匿名使用者存取](lync-server-2013-enable-or-disable-anonymous-user-access.md)

  - [在 Lync Server 2013 中指派會議原則以支援匿名使用者](lync-server-2013-assign-conferencing-policies-to-support-anonymous-users.md)

