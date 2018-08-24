---
title: Lync Server 2013：啟用或停用遠端使用者存取
TOCTitle: 啟用或停用遠端使用者存取
ms:assetid: cd9d3ddc-4839-457a-86d9-b15413e74002
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182586(v=OCS.15)
ms:contentKeyID: 49292346
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中啟用或停用遠端使用者存取

 

_**上次修改主題的時間：** 2013-02-23_

遠端使用者是貴組織內的使用者，他們在組織內擁有常設性的 Active Directory 身分。當遠端使用者未連接組織網路時，通常會使用虛擬私人網路 (VPN) 從您網路之外登入 Lync Server。他們包括在家工作或在外出差的員工或是其他遠端工作者 (例如受信任的廠商)，這些人員均擁有企業認證。如果您對遠端使用者啟用遠端使用者存取，擁有網際網路連線的受支援遠端使用者即可透過 Lync Server 與內部使用者共同作業，而不需要使用 VPN 連線。

若要支援遠端使用者存取，您必須啟用遠端使用者存取。當您啟用遠端使用者存取時，可以為整個組織啟用此功能。如果您在日後想要暫時或永久禁止遠端使用者存取，可以為組織停用此功能。請使用本節中的程序來為組織啟用或停用遠端使用者存取。

> [!NOTE]  
> 啟用遠端使用者存取只會指定執行 Access Edge Service 的伺服器支援遠端使用者通訊，但除非您另外設定至少一個遠端使用者存取的使用管理原則，否則遠端使用者無法參與組織內的立即訊息 (IM) 或會議。 套用到某原則層級的 Lync Server 原則設定，可能會覆寫套用到其他原則層級的設定。Lync Server 原則的優先順序是使用者原則 (影響力最大) 會覆寫網站原則，網站原則則會覆寫全域原則 (影響力最小)。亦即，愈接近原則所影響之物件的原則設定，對物件的影響力愈大。如需關於設定遠端使用者存取之使用原則的詳細資訊，請參閱 <a href="lync-server-2013-configure-policies-to-control-remote-user-access.md">在 Lync Server 2013 中設定原則以控制遠端使用者存取</a>。



## 啟用或停用貴組織的遠端使用者存取

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 \[同盟和外部存取\] 和 \[Access Edge 設定\] 。

4.  在 **\[Access Edge 設定\]** 頁面上，依序按一下 **\[全域\]** 、 **\[編輯\]** ，然後按一下 **\[顯示詳細資料\]** 。

5.  在 **\[編輯 Access Edge 設定\]** 中，執行下列其中一項：
    
      - 若要啟用組織的遠端使用者存取，請選取 \[啟用遠端使用者存取\] 核取方塊。
    
      - 若要停用組織的遠端使用者存取，請清除 \[啟用遠端使用者存取\] 核取方塊。

6.  按一下 \[認可\] 。

若要允許遠端使用者登入執行 Lync Server 的伺服器，您必須另外設定至少一個外部存取原則以支援遠端使用者存取。如需詳細資訊，請參閱部署文件或作業文件中的 [在 Lync Server 2013 中設定原則以控制遠端使用者存取](lync-server-2013-configure-policies-to-control-remote-user-access.md)。

## 使用 Windows PowerShell Cmdlet 啟用或停用遠端使用者存取

遠端使用者存取可使用 Windows PowerShell 和 Set-CsAccessEdgeConfiguration Cmdlet 加以管理。此 Cmdlet 可從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 啟用遠端使用者存取

  - 若要啟用遠端使用者存取，請將 **AllowOutsideUsers** 屬性的值設為 True ($True)：
    
        Set-CsAccessEdgeConfiguration -AllowOutsideUsers $True

## 停用遠端使用者存取

  - 若要停用遠端使用者存取，請將 **AllowOutsideUsers** 屬性的值設為 False ($False)：
    
        Set-CsAccessEdgeConfiguration -AllowOutsideUsers $False

