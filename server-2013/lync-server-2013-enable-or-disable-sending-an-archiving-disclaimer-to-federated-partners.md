---
title: Lync Server 2013：啟用或停用傳送封存免責聲明至同盟合作夥伴的功能
TOCTitle: 啟用或停用傳送封存免責聲明至同盟合作夥伴的功能
ms:assetid: c8e9a2fa-9dc1-4e4d-919f-56ece8004864
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182584(v=OCS.15)
ms:contentKeyID: 49292290
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中啟用或停用傳送封存免責聲明至同盟合作夥伴的功能

 

_**上次修改主題的時間：** 2013-02-23_

您部署 Edge Server 並啟用組織的同盟時，應該已經指定是否自動將封存免責聲明傳送給同盟協力廠商。如果您封存外部通訊，則應該啟用傳送封存免責聲明。您可以使用本主題中的程序來變更該項設定。

> [!NOTE]  
> 以下程序假設您已為組織啟用同盟。如需啟用同盟關係的詳細資訊，請參閱部署或作業文件中的 <a href="lync-server-2013-enable-or-disable-remote-user-access.md">在 Lync Server 2013 中啟用或停用遠端使用者存取</a>。



## 啟用或停用將封存免責聲明傳送給同盟協力廠商

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  按一下左導覽列中的 **\[外部使用者存取\]** ，然後再按一下 **\[Access Edge 設定\]** 。

4.  在 **\[Access Edge 設定\]** 索引標籤中，依序按一下 **\[全域\]** 、 **\[編輯\]** 和 **\[顯示詳細資料\]** 。

5.  在 **\[編輯 Access Edge 設定\]** 的 **\[啟用與同盟使用者的通訊\]** 底下，選取或清除 **\[將封存免責聲明傳送給同盟協力廠商\]** 核取方塊即可啟用或停用自動傳送封存免責聲明。

6.  按一下 \[認可\] 。

若要允許同盟使用者和 Lync Server 2013 部署中的使用者共同作業，您必須另外設定至少一個外部存取原則才能支援同盟使用者存取。如需詳細資訊，請參閱部署文件或作業文件中的 [在 Lync Server 2013 中管理 XMPP 同盟夥伴](lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md)。如需控制特定同盟網域之存取的詳細資訊，請參閱部署文件或作業文件中的 [在 Lync Server 2013 中針對允許的外部網域設定支援](lync-server-2013-configure-support-for-allowed-external-domains.md)。

## 使用 Windows PowerShell Cmdlet 啟用或停用封存免責聲明

您可以使用 Windows PowerShell和 Set-CsAccessEdgeConfiguration Cmdlet 來管理封存免責聲明的使用。此 Cmdlet 可從 Lync Server 2013 管理命令介面或從 Windows PowerShell的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 啟用封存免責聲明

  - 若要啟用封存免責聲明，請將 **EnableArchivingDisclaimer** 屬性的值設為 True ($True)：
    
        Set-CsAccessEdgeConfiguration -EnableArchivingDisclaimer $True

## 停用封存免責聲明

  - 若要停用封存免責聲明，請將 **EnableArchivingDisclaimer** 屬性的值設為 False ($False)：
    
        Set-CsAccessEdgeConfiguration -EnableArchivingDisclaimer $False

