---
title: 刪除現有 Web 服務組態設定
TOCTitle: 刪除現有 Web 服務組態設定
ms:assetid: c2b96f4c-4b07-48e6-9ca6-55bc0e0cf5a1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182582(v=OCS.15)
ms:contentKeyID: 49292220
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除現有 Web 服務組態設定

 

_**上次修改主題的時間：** 2013-02-23_

請依照下列步驟刪除 Web 服務原則。

## 若要刪除 Web 服務原則

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[安全性\]**，然後按一下 **\[Web 服務\]**。

4.  在 **\[Web 服務\]** 頁面上的搜尋欄位中，輸入您要刪除之原則的全部或部分名稱。

5.  在原則清單中，按一下您要的原則，再按一下 **\[編輯\]**，然後按一下 **\[刪除\]**。

6.  按一下 \[確定\] 。

## 使用 Lync Server 管理命令介面 Cmdlet 刪除新的 Web 服務組態設定

您也可以使用 Lync Server 管理命令介面和 **Remove-CsWebServiceConfiguration** Cmdlet 刪除 Web 服務組態設定。您可以從 Lync Server 2013 管理命令介面 或從 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 若要刪除特定的 Web 服務組態設定集合

  - 下列命令會移除套用至 Redmond 網站的 Web 服務安全性設定：
    
        Remove-CsWebServiceConfiguration -Identity "site:Redmond"

## 若要刪除套用至網站範圍的所有 Web 服務組態設定

  - 下列命令會移除套用至服務範圍的所有 Web 服務安全性設定：
    
        Get-CsWebServiceConfiguration -Filter "service:*" | Remove-CsWebServiceConfiguration

## 若要刪除所有允許憑證驗證的 Web 服務組態設定

  - 下列命令會移除所有允許使用憑證驗證的 Web 服務安全性設定：
    
        Get-CsWebServiceConfiguration | Where-Object {$_.UseCertificateAuth -eq $True} | Remove-CsWebServiceConfiguration

如需詳細資訊，請參閱 [Remove-CsWebServiceConfiguration](remove-cswebserviceconfiguration.md)。

## 請參閱

#### 其他資源

[在 Lync Server 2013 控制台中設定驗證](lync-server-2013-configuring-authentication-in-the-lync-server-control-panel.md)

