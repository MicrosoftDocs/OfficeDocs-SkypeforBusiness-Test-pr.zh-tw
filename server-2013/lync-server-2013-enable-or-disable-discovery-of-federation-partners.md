---
title: Lync Server 2013：啟用或停用探索同盟協力廠商
TOCTitle: 啟用或停用探索同盟協力廠商
ms:assetid: 91fd036b-b1af-47cf-b1cf-0aa0a783c2aa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182550(v=OCS.15)
ms:contentKeyID: 49291674
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中啟用或停用探索同盟協力廠商

 

_**上次修改主題的時間：** 2013-02-23_

當您部署 Edge Server 並為組織啟用同盟時，應已指定是否要支援自動探索同盟協力廠商網域。您可以使用本主題中的程序來變更該項設定。

> [!NOTE]  
> 以下程序假設您已為組織啟用同盟。如需啟用同盟關係的詳細資訊，請參閱部署或作業文件中的 <a href="lync-server-2013-enable-or-disable-remote-user-access.md">在 Lync Server 2013 中啟用或停用遠端使用者存取</a>。



## 若要為組織啟用或停用自動探索同盟網域

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  按一下左導覽列中的 **\[外部使用者存取\]** ，然後再按一下 **\[Access Edge 設定\]** 。

4.  在 **\[Access Edge 設定\]** 頁面上，依序按一下 **\[全域\]** 、 **\[編輯\]** ，然後按一下 **\[顯示詳細資料\]** 。

5.  在 **\[編輯 Access Edge 設定\]** 的 **\[啟用與同盟使用者的通訊\]** 下方，選取或清除 **\[啟用協力廠商網域探索\]** 核取方塊以啟用或停用協力廠商網域的自動探索。

6.  按一下 \[認可\] 。

若要允許同盟使用者和 Lync Server 部署中的使用者共同作業，您必須另外設定至少一個外部存取原則才能支援同盟使用者存取。如需詳細資訊，請參閱部署文件或作業文件中的 [在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)。如需關於控制特定同盟網域之存取的詳細資訊，請參閱作業文件中的 [在 Lync Server 2013 中管理組織的 SIP 同盟網域](lync-server-2013-manage-sip-federated-domains-for-your-organization.md)、 [在 Lync Server 2013 中管理組織的 SIP 同盟提供者](lync-server-2013-manage-sip-federated-providers-for-your-organization.md)及 [在 Lync Server 2013 中管理 XMPP 同盟夥伴](lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md)。

## 使用 Windows PowerShell Cmdlet 來啟用或停用同盟協力廠商的探索

同盟協力廠商的探索可以使用 Windows PowerShell 和 Set-CsAccessEdgeConfiguration Cmdlet 來管理。此 Cmdlet 可以從 Lync Server 2013 管理命令介面 或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 啟用同盟協力廠商的探索

  - 若要啟用同盟協力廠商的探索，請將 **EnablePartnerDiscovery** 屬性的值設定為 True ($True)。請注意，您必須啟用 DNS SRV 路由傳送，才能變更此屬性值。
    
        Set-CsAccessEdgeConfiguration -UseDnsSrvRouting -EnablePartnerDiscovery $True

## 停用同盟協力廠商的探索

  - 若要停用同盟協力廠商的探索，請將 **EnablePartnerDiscovery** 屬性的值設定為 False ($False)：
    
        Set-CsAccessEdgeConfiguration -UseDnsSrvRouting -EnablePartnerDiscovery $False

