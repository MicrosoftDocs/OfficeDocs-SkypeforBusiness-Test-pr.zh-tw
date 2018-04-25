---
title: 刪除現有登錄器組態設定
TOCTitle: 刪除現有登錄器組態設定
ms:assetid: ae43cd75-cae4-4f78-b037-779a2cdb583b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182571(v=OCS.15)
ms:contentKeyID: 49291992
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除現有登錄器組態設定

 

_**上次修改主題的時間：** 2013-02-23_

請依照下列步驟刪除登錄器。

## 若要刪除登錄器

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[安全性\]**，然後按一下 **\[登錄器\]**。

4.  在 **\[登錄器\]** 頁面上的搜尋欄位中，輸入您要刪除之登錄器的全部或部分名稱。

5.  在清單中，依序按一下所要的登錄器、**\[編輯\]** 和 **\[刪除\]**。

6.  按一下 \[確定\] 。

## 使用 Lync Server 管理命令介面 Cmdlet 來移除登錄器組態設定

您也可以使用 Lync Server 管理命令介面與 **Remove-CsProxyConfiguration** Cmdlet 來刪除登錄器組態設定。您可從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 移除特定的登錄器安全性設定組

  - 下列命令可移除套用至 Edge Server atl-edge-011.litwareinc.com 的登錄器安全性設定：
    
        Remove-CsProxyConfiguration -Identity service:EdgeServer:atl-edge-011.litwareinc.com

## 移除套用至此網站範圍的登錄器安全性設定

  - 下列命令可移除套用至登錄器服務的所有登錄器安全性設定：
    
        Get-CsProxyConfiguration -Filter "service:Registrar:*" | Remove-CsProxyConfiguration

## 移除允許 NTLM 驗證的所有登錄器安全性設定

  - 下列命令可移除允許使用 NTLM 進行用戶端驗證的所有登錄器安全性設定：
    
        Get-CsProxyConfiguration | Where-Object {$_.UseNtlmForClientToProxyAuth -eq $True}| Remove-CsProxyConfiguration

如需詳細資訊，請參閱 [Remove-CsProxyConfiguration](remove-csproxyconfiguration.md)。

