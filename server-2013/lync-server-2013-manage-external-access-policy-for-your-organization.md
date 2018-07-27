---
title: Lync Server 2013：管理組織的外部使用存取原則
TOCTitle: 管理組織的外部使用存取原則
ms:assetid: 5571811e-34c8-443a-b94c-1ab5d4275581
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520995(v=OCS.15)
ms:contentKeyID: 49290957
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中管理外部使用存取原則

 

_**上次修改主題的時間：** 2013-10-07_

部署一或多部 Edge Server 之後，您必須為組織啟用將支援的外部存取類型。

依預設，不會將任何原則設定為支援外部使用者存取 (包括遠端使用者存取、同盟網域使用者存取)，即使您已經為組織啟用外部使用者存取支援也一樣。若要控制外部使用者存取的使用，您必須設定一或多個原則，並為每個原則指定支援的外部使用者存取類型。您可以使用下列原則範圍來進行建立和設定。預設會建立全域原則，但無法加以刪除。

  - **全域原則**   全域原則是在您部署 Edge Server 時所建立。依預設，全域原則中不會啟用任何外部使用者存取選項。若要在全域層級支援外部使用者存取，您可以設定全域原則來支援一或多個外部使用者存取選項類型。全域原則會套用至組織內所有使用者，但網站原則和使用者原則優先於全域原則。如果刪除全域原則，並不代表將其移除，而是將其重設為預設設定。

  - **網站原則**   您可以建立和設定一或多個網站原則，以對特定網站限制外部使用者存取的支援。網站原則中的設定優先於全域原則，但僅限該網站原則所涵蓋的特定網站。例如，如果您在全域原則中啟用了遠端使用者存取，您可以指定網站原則以對特定網站停用遠端使用者存取。依預設，網站原則會套用至該網站的所有使用者，但您可以將使用者原則指派給個別使用者，以覆寫網站原則設定。

  - **使用者原則**   您可以建立和設定一或多個使用者原則，以對特定使用者限制遠端使用者存取支援。使用者原則中的設定優先於全域與網站原則，但僅限指派該使用者原則的特定使用者。例如，如果您在全域原則和網站原則中啟用了遠端使用者存取，您可以指定使用者原則以停用遠端使用者存取，然後將該使用者原則指派給特定使用者。如果您建立使用者原則，必須將其套用至一或多位使用者，該原則才能生效。

> [!IMPORTANT]  
> 套用到某原則層級的 Lync Server 原則設定，可能會覆寫套用到其他原則層級的設定。Lync Server 原則的優先順序是使用者原則 (影響力最大) 會覆寫網站原則，網站原則則會覆寫全域原則 (影響力最小)。亦即，愈接近原則所影響之物件的原則設定，對物件的影響力愈大。



這些選項包含下列外部存取類型：

  - **啟用與同盟使用者的通訊**    如果您想要支援使用者存取同盟協力廠商網域，可啟用此選項。此設定讓使用者能夠與其他 SIP 同盟網域通訊，以及與像是 Microsoft Office 365 的裝載提供者通訊。選取此設定，讓您能夠選取選項來允許與 XMPP 同盟網域進行通訊。
    
    做為選項，如果您先選取 **\[啟用與同盟使用者的通訊\]** ，則可選取 **\[啟用與 XMPP 同盟協力廠商的通訊\]** 。XMPP 同盟是與使用 Extensible Messaging and Presence Protocol (XMPP) 的組織同盟。
    
    > [!NOTE]  
    > 如果您啟用 XMPP 同盟，也必須在 拓撲產生器的 Edge 集區設定區段中選取以部署 <strong>[XMPP同盟]</strong> 。針對 XMPP 同盟進行設定，會在 Edge Server 上部署 XMPP Proxy 且在 前端伺服器上部署 XMPP 閘道。
    


  - **啟用與遠端使用者的通訊**    如果您想要讓位於防火牆外部的組織內使用者 (例如在家工作與出差的使用者) 連線至 Lync Server，可啟用此選項。

  - **啟用與公用使用者的通訊**    如果您想要讓內部使用者能夠與公用 IM 提供者連絡人聯絡 (例如由 Windows Live、Yahoo\! 及 America Online (AOL) 所提供的連絡人)，可啟用此選項。
    
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


> [!NOTE]  
> 除了啟用外部使用者存取支援，您還必須設定相關原則以控制組織外部使用者存取的使用，接著再為使用者提供任何類型的外部使用者存取。如需有關建立、設定及套用外部使用者存取原則的詳細資訊，請參閱＜ <a href="lync-server-2013-enable-or-disable-remote-user-access.md">在 Lync Server 2013 中啟用或停用遠端使用者存取</a>＞。



**使用 Windows PowerShell Cmdlet 檢視外部存取原則**

  - 您可以使用 Lync Server 管理命令介面和 **Get-CsExternalAccessPolicy** Cmdlet，檢視外部存取原則。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。 如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。
    
    若要檢視關於您所有外部存取原則的資訊，請在 Lync Server 管理命令介面中輸入下列命令，然後按 ENTER 鍵：
    
        Get-CsExternalAccessPolicy
    
    此命令會傳回與下列相似的資訊：
    
        Identity                          : Global
        Description                       :
        EnableFederationAccess            : False
        EnableXmppAccess                  : False
        EnablePublicCloudAccess           : False
        EnablePublicCloudAudioVideoAccess : False
        EnableOutsideAccess               : False

## 本章節內容

  - [在 Lync Server 2013 中設定控制同盟使用者存取的原則](lync-server-2013-configure-policies-to-control-federated-user-access.md)

  - [在 Lync Server 2013 中設定原則以控制 XMPP 同盟使用者存取](lync-server-2013-configure-policies-to-control-xmpp-federated-user-access.md)

  - [在 Lync Server 2013 中設定原則以控制遠端使用者存取](lync-server-2013-configure-policies-to-control-remote-user-access.md)

  - [在 Lync Server 2013 中設定原則以控制公用使用者存取](lync-server-2013-configure-policies-to-control-public-user-access.md)

  - [在 Lync Server 2013 中將外部使用者存取原則指派給擁有 Lync 功能的使用者](lync-server-2013-assign-an-external-user-access-policy-to-a-lync-enabled-user.md)

  - [在 Lync Server 2013 中重設或刪除外部使用者存取原則](lync-server-2013-resetting-or-deleting-external-user-access-policies.md)

