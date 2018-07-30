---
title: Lync Server 2013：啟用或停用匿名使用者存取
TOCTitle: 啟用或停用匿名使用者存取
ms:assetid: f10c19e6-b6f9-4d26-9923-0165f36e4af8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619192(v=OCS.15)
ms:contentKeyID: 49292769
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中啟用或停用匿名使用者存取

 

_**上次修改主題的時間：** 2013-02-23_

匿名使用者就是在貴組織的 Active Directory 網域服務 中或在支援的同盟網域中沒有使用者帳戶的使用者，可以受邀在遠端參加內部部署會議。只要允許匿名參與會議，即可讓匿名使用者 (就是僅透過會議金鑰驗證身分的使用者) 加入會議。您必須啟用貴組織的匿名參與功能，才可允許匿名參與。

如果之後想要暫時或永久防止匿名使用者存取，您可以停用貴組織的該項功能。使用本節中的程序來停用貴組織的匿名使用者存取。

> [!NOTE]  
> 啟用貴組織的匿名使用者存取，只是指定執行 Access Edge 服務的伺服器支援匿名使用者存取。在您也設定至少一項會議原則並將該原則套用至一或多個使用者或使用者群組之前，匿名使用者無法參與貴組織的任何會議。唯一可以邀請匿名使用者參加會議的使用者，就是已被指派設定為支援匿名使用者之會議原則的使用者。如需設定會議員則以支持邀請匿名使用者的詳細資訊，請參閱 <a href="lync-server-2013-conferencing-policies.md">Lync Server 2013 中的會議原則</a>。



## 啟用或停用貴組織的匿名使用者存取

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[外部使用者存取\]** ，然後按一下 **\[Access Edge 設定\]** 。

4.  在 **\[Access Edge 設定\]** 頁面上，依序按一下 **\[全域\]** 、 **\[編輯\]** ，然後按一下 **\[顯示詳細資料\]** 。

5.  在 **\[編輯 Access Edge 設定\]** 中，執行下列其中一項：
    
      - 若要啟用貴組織的匿名使用者存取，請選取 \[啟用與匿名使用者的通訊\] 核取方塊。
    
      - 若要停用貴組織的匿名使用者存取，請清除 \[啟用與匿名使用者的通訊\] 核取方塊。

6.  按一下 \[認可\] 。

## 使用 Windows PowerShell Cmdlet 啟用或停用匿名使用者存取

您可使用 Windows PowerShell 與 **Set-CsAccessEdgeConfiguration** Cmdlet 管理匿名使用者存取。您可從 Lync Server 2013 管理命令介面或 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 啟用匿名使用者存取

  - 若要啟用匿名使用者存取，請將 **AllowAnonymousUsers** 屬性值設定為 True ($True)：
    
        Set-CsAccessEdgeConfiguration -AllowAnonymousUsers $True

## 停用匿名使用者存取

  - 若要停用匿名使用者存取，請將 **AllowAnonymousUsers** 屬性值設定為 False ($False)：
    
        Set-CsAccessEdgeConfiguration -AllowAnonymousUsers $False

## 請參閱

#### 概念

[Lync Server 2013 中的會議原則設定參考](lync-server-2013-conferencing-policy-settings-reference.md)

