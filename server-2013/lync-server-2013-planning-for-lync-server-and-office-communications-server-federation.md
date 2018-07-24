---
title: 規劃 Lync Server 與 Office Communications Server 同盟
TOCTitle: 規劃 Lync Server 與 Office Communications Server 同盟
ms:assetid: c9eaf06b-054f-41a4-ad0c-499400d6c4c7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205335(v=OCS.15)
ms:contentKeyID: 49292316
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 規劃 Lync Server 與 Office Communications Server 同盟

 

_**上次修改主題的時間：** 2013-02-13_

Microsoft Lync Server 2013、Lync Server 2010 與 Office Communications Server 之間的同盟可支援對等通訊和多方通訊。對等交談可以提昇為多方交談，進而成為臨時舉行的會議。會議 (Web 會議或音訊/視訊會議) 可以安排為包含您組織中的連絡人，以及您同盟合作夥伴中的連絡人。

同盟最初出現於 Microsoft Office Live Communications Server 2005 中，當時可支援一種同盟，即直接同盟。若要進行直接同盟，必須知道同盟協力廠商的工作階段初始通訊協定 (SIP) 網域，以及合作夥伴 Edge Server 的完整網域名稱 (FQDN)。Live Communications Server 2005 含 SP1 中引進了更多同盟類型，那些同盟類型全都需要同盟合作夥伴公佈網域名稱系統 (DNS) SRV 記錄來供人尋找他們的 Edge Server。該版本所用的術語包括：

  - *開放式增強型同盟*：接受任何 SIP 網域名稱，並使用 DNS SRV 尋找合作夥伴的 Edge Server

  - *增強型同盟*：設定合作夥伴的 SIP 網域名稱做為貴組織的同盟合作夥伴，並使用 DNS SRV 尋找合作夥伴的 Edge Server

  - *直接同盟*：設定合作夥伴的 SIP 網域名稱以及合作夥伴 Edge Server 的 FQDN

  - *伺服器允許清單*：接受任何網域，使用 DNS SRV 尋找裝載提供者或公用立即訊息 (IM) 連線提供者的 Edge Server

Microsoft Office Communications Server 2007 中引進更新後的同盟類型命名方式，以更清楚指出每種同盟類型實際達到的效果：

  - 開放式增強型同盟變成為「探索到的協力廠商網域」

  - 增強型同盟變成為「允許的協力廠商網域」

  - 直接同盟變成為「允許的協力廠商伺服器」

  - 伺服器允許清單變成為「裝載提供者」和「公用 IM 提供者」

Microsoft Lync Server 2010 中對「裝載提供者」引進更狹義的名稱，以配合 Microsoft Lync Online 2010 和 Microsoft Office 365，同時也使它必須受「允許的協力廠商網域」同盟類型所定義之相同允許清單的約束。

啟用 Microsoft Lync Server 2013、Lync Server 2010 與 Office Communications Server 之間的同盟會使用 Edge Server 及反向 Proxy 來強制執行您所定義的規則和允許的協力廠商網域。從規劃的角度而言，要與其他 Lync Server 同盟，Office Communications Server 有下列條件：

  - 在拓撲產生器中啟用同盟。如需詳細資訊，請參閱部署的[在 Lync Server 2013 中設定 SIP 同盟、XMPP 同盟及 Public Instant Messaging](lync-server-2013-configuring-sip-federation-xmpp-federation-and-public-instant-messaging.md)主題。

  - 判斷您的同盟網域探索需求：
    
       如需手動設定同盟，您必須具備合作夥伴的 Edge Server 完整網域名稱 (FQDN) 和網域名稱，或線上網域名稱 (這輸入於 Lync Server 控制台 \> \[同盟及外部存取\]\> \[SIP 同盟網域\]。請「新增」原則或「編輯」現有的原則，以依 FQDN 來允許或封鎖網域。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>手動設定同盟合作夥伴的 Edge Server 很容易會因為合作夥伴變更了 Edge Server IP 位址而失敗。</td>
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
        <td>若是新的 SIP 同盟網域，您必須為 Microsoft Lync Online、Microsoft Office 365 提供 [網域名稱 (或 FQDN)]。若是 Microsoft Lync Server 2013、Lync Server 2010 及 Office Communications Server，您也必須提供 [Access Edge Service (FQDN)]</td>
        </tr>
        </tbody>
        </table>
    
       若是探索到的協力廠商同盟 (合作夥伴可以探索您的 Edge Server)，您需在外部 DNS (\_sipfederationtls.\_tcp.contoso.com) 中建立一筆指向連接埠 5061 的 SRV 記錄以及您 Edge Server 的主機 (A) 記錄
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果您正支援 Windows Phone、Apple iPhone、iPad 或其他 Apple 裝置上的 Microsoft Lync Mobile 用戶端，且使用推播通知服務或推播通知服務，您必須針對您每個有 Lync Mobile 用戶端的 SIP 網域來規劃 _sipfederationtls._tcp. <em>&lt;SIP 網域&gt;</em> SRV 記錄。Android 和 Nokia Symbian Lync Mobile 並不使用推入通知，因此不受此條件限制。</td>
        </tr>
        </tbody>
        </table>


  - 設定外部使用者存取原則來支援同盟網域

  - 針對工作階段初始通訊協定 (SIP)、Web 會議及音訊/視訊開啟防火牆連接埠，以配合您要啟用的同盟或聯繫。如需詳細資訊，請參閱[決定 Lync Server 2013 的外部 A/V 防火牆和連接埠需求](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md)

下列資訊將可協助您定義出要和 Microsoft Lync Server 2013 與 Lync Server 2010 進行同盟時，所必須符合的憑證、連接埠/通訊協定和 DNS 需求。

如果您已進行 Microsoft Lync Server 2013 Edge Server 的規劃或部署，規劃憑證、防火牆與連接埠/通訊協定需求和 DNS 需求，通常會是很直觀的程序。由於同盟是一項使用到現有 Edge Server 的額外功能，因此這些規劃需求通常已在規劃與部署 Edge Server 的過程中獲得滿足。您應該使用下列表格來判斷您的需求是否已獲得滿足，並據此變更連接埠/通訊協定和 DNS。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您有 Edge Server 的集區，且正在與 Lync Server 2013 或 Lync Server 2010 合作夥伴進行同盟，您便可以在 Edge Server 的對內與對外處，使用 DNS 負載平衡或硬體負載平衡器。如果您正在與 Office Communications Server 2007 或 Office Communications Server 2007 R2 進行同盟，則硬體負載平衡將能在 Edge Server、Office Communications Server 2007 和 Office Communications Server 2007 R2 感測不到 DNS 負載平衡時提供容錯移轉支援。合作夥伴的 Edge Server 將與您集區中第一個回應的 Edge Server 建立通訊。如果該 Edge Server 失敗，通訊不會自動進行容錯移轉。</td>
</tr>
</tbody>
</table>


憑證需求通常是透過規劃您所選 Edge Server 或集區 Edge Server 計畫的憑證而獲得滿足。

## 本章節內容

  - [憑證摘要 - SIP、XMPP 同盟和公用立即訊息](lync-server-2013-certificate-summary-sip-xmpp-federation-and-public-instant-messaging.md)

  - [連接埠摘要 - SIP、XMPP 同盟和公用立即訊息](lync-server-2013-port-summary-sip-xmpp-federation-and-public-instant-messaging.md)

  - [DNS 摘要 - SIP、XMPP 同盟和公用立即訊息](lync-server-2013-dns-summary-sip-xmpp-federation-and-public-instant-messaging.md)

## 請參閱

#### 工作

[在 Lync Server 2013 中設定控制同盟使用者存取的原則](lync-server-2013-configure-policies-to-control-federated-user-access.md)  

#### 概念

[Lync Server 2013 中的外部使用者存取案例](lync-server-2013-scenarios-for-external-user-access.md)  
[決定 Lync Server 2013 的外部 A/V 防火牆和連接埠需求](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md)  
[針對 Lync Server 2013 判定 DNS 需求](lync-server-2013-determine-dns-requirements.md)  

#### 其他資源

[在 Lync Server 2013 中管理組織的 Access Edge 設定](lync-server-2013-manage-access-edge-configuration-for-your-organization.md)  
[在 Lync Server 2013 中管理組織的 SIP 同盟網域](lync-server-2013-manage-sip-federated-domains-for-your-organization.md)  
[在 Lync Server 2013 中管理組織的 SIP 同盟提供者](lync-server-2013-manage-sip-federated-providers-for-your-organization.md)

