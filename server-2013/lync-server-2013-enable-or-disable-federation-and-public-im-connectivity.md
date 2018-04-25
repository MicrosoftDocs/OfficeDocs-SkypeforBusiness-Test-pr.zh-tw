---
title: Lync Server 2013：啟用或停用同盟與公用 IM 連線
TOCTitle: 啟用或停用同盟與公用 IM 連線
ms:assetid: 8ec58f4b-9f6d-47b4-a187-d18a83fe4577
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182549(v=OCS.15)
ms:contentKeyID: 49291633
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線

 

_**上次修改主題的時間：** 2013-06-24_

同盟支援是讓擁有受信任客戶或合作夥伴組織 (包括您支援的合作夥伴網域和公用立即訊息 (IM) 提供者的使用者) 之帳戶的使用者，與您組織內的使用者共同作業時必要的支援。同盟也必須使用裝載的 Exchange 服務提供者，才可以提供語音信箱給 Enterprise Voice 使用者，該使用者的信箱位在裝載的 Exchange 服務上 (例如 Microsoft Exchange Online)。當您與這些外部網域建立了信任關係時，可以授權這些網域內的使用者存取您的部署並參與 Lync Server 通訊。此信任關係即稱為「同盟」，它與 Active Directory 信任關係不相關，也沒有相依性。

若要支援同盟網域的使用者進行存取，您必須啟用同盟。如果您針對組織啟用同盟，還必須指定是否實作下列選項：

  - **啟用協力廠商網域探索**    如果您啟用此選項， Lync Server 就會使用網域名稱系統 (DNS) 記錄，嘗試探索未列在允許的網域清單中的網域、自動評估來自探索之同盟協力廠商的傳入流量，以及根據信任層級、流量和系統管理員設定來限制或封鎖該流量。如果您未選取此選項，則只會針對包含在允許的網域清單中的網域使用者啟用同盟使用者存取。無論是否選取此選項，您都可以指定封鎖或允許個別網域，包括限制存取同盟網域中執行 Access Edge 服務的特定伺服器。如需關於控制同盟網域之存取的詳細資訊，請參閱＜ [在 Lync Server 2013 中針對允許的外部網域設定支援](lync-server-2013-configure-support-for-allowed-external-domains.md)＞。

  - **傳送封存免責聲明給同盟協力廠商**     將免責聲明通知傳送給同盟協力廠商，表示您的部署中已具備封存功能。如果您支援封存與同盟協力廠商網域的外部通訊，則應該啟用封存免責聲明通知，警告協力廠商將會封存其訊息。

如果您之後想要暫時或永久阻止同盟網域的使用者存取，則可以停用組織的同盟。利用本節中的程序即可啟用或停用組織的同盟使用者存取，包括為組織指定要支援的適當同盟選項。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>啟用貴組織的同盟，只是指定執行 Access Edge 服務的伺服器支援同盟網域的路由。除非您也至少設定一個原則來支援同盟使用者存取，否則同盟網域中的使用者無法參與您組織內的 IM 或會議。除非您也至少設定一個原則來支援公用 IM 連線，否則公用 IM 服務提供者的使用者無法參與您組織內的 IM 或會議。除非您設定提供路由資訊之裝載的語音信箱原則，否則 Lync Server 無法為信箱位於裝載之 Exchange 服務的使用者，提供來電接聽、Outlook 語音存取 (包括語音信箱) 或自動語音應答服務。如需關於設定與其他組織中的同盟網域使用者進行通訊之原則的詳細資訊，請參閱作業文件中的 <a href="lync-server-2013-manage-sip-federated-domains-for-your-organization.md">在 Lync Server 2013 中管理組織的 SIP 同盟網域</a>。另外，如果您想要支援與 IM 服務提供者的使用者進行通訊，則必須設定原則來支援此通訊，同時針對要支援的個別服務提供者設定支援。如需詳細資訊，請參閱作業文件中的 <a href="lync-server-2013-manage-sip-federated-providers-for-your-organization.md">在 Lync Server 2013 中管理組織的 SIP 同盟提供者</a>。如需關於建立裝載之語音信箱原則的詳細資訊，請參閱部署文件中的 <a href="lync-server-2013-manage-hosted-voice-mail-policies.md">在 Lync Server 2013 中管理裝載語音信箱原則</a>。</td>
</tr>
</tbody>
</table>


## 啟用或停用組織的同盟使用者存取

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[外部使用者存取\]** ，然後按一下 **\[Access Edge 設定\]** 。

4.  在 **\[Access Edge 設定\]** 頁面上，依序按一下 **\[全域\]** 、 **\[編輯\]** ，然後按一下 **\[顯示詳細資料\]** 。

5.  在 **\[編輯 Access Edge 設定\]** 中，執行下列其中一項：
    
      - 若要啟用組織的同盟使用者存取，請選取 \[啟用與同盟使用者的通訊\] 核取方塊。
    
      - 若要停用組織的同盟使用者存取，請清除 \[啟用與同盟使用者的通訊\] 核取方塊。

6.  如果您已選取 \[啟用與同盟使用者的通訊\] 核取方塊，請執行下列動作：
    
    1.  如果您要支援自動探索協力廠商網域，請選取 \[啟用協力廠商網域探索\] 核取方塊。
    
    2.  如果您的組織支援外部通訊封存，請選取 \[將封存免責聲明傳送給同盟協力廠商\] 核取方塊。

7.  按一下 \[認可\] 。

若要讓同盟使用者與 Lync Server 2013 部署中的使用者共同作業，您還必須至少設定一個外部存取原則來支援同盟使用者存取。如需詳細資訊，請參閱 部署文件或作業文件中的 [在 Lync Server 2013 中設定控制同盟使用者存取的原則](lync-server-2013-configure-policies-to-control-federated-user-access.md)。若要控制特定同盟網域的存取，請參閱部署文件或作業文件中的 [在 Lync Server 2013 中針對允許的外部網域設定支援](lync-server-2013-configure-support-for-allowed-external-domains.md)。

## 使用 Windows PowerShell Cmdlet 啟用和停用同盟與公用 IM 連線

同盟與公用 IM 連線也可以使用 Windows PowerShell 和 Set-CsAccessEdgeConfiguration Cmdlet 來管理。此 Cmdlet 可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。 如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 啟用同盟和公用 IM 連線

  - 若要啟用同盟和公用 IM 連線，請將 **AllowFederatedUsers** 屬性值設為 True ($True)：
    
        Set-CsAccessEdgeConfiguration -AllowFederatedUsers $True

## 停用同盟和公用 IM 連線

  - 若要停用同盟和公用 IM 連線，請將 **AllowFederatedUsers** 屬性值設為 False ($False)：
    
        Set-CsAccessEdgeConfiguration -AllowFederatedUsers $False

