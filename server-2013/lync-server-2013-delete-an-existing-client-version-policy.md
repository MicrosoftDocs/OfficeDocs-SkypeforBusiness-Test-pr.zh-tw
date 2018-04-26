---
title: 刪除現有的用戶端版本原則
TOCTitle: 刪除現有的用戶端版本原則
ms:assetid: b88aaa25-97ff-4eb6-bd34-b97332cd6890
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ923064(v=OCS.15)
ms:contentKeyID: 52056209
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除現有的用戶端版本原則

 

_**上次修改主題的時間：** 2013-02-23_

如果您想要刪除先前設定的戶端版本原則，您可以從 Lync Server 2013 控制台或 Lync Server 2013 管理命令介面予以刪除。

## 使用 Lync Server 控制台刪除用戶端版本原則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列，按一下 \[用戶端\]，然後按一下 \[用戶端版本原則\] 導覽按鈕。

4.  在「用戶端版本原則」頁面，選取您要刪除的用戶端版本原則，按一下 \[編輯\]，然後按一下 \[刪除\]。

## 使用 Windows PowerShell Cmdlet 刪除用戶端版本原則

您可以使用 **Remove-CsClientVersionPolicy** Cmdlet 刪除用戶端版本原則。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 移除特定的用戶端版本原則

  - 此命令會刪除套用至 Redmond 網站的用戶端版本原則：
    
        Remove-CsClientVersionPolicy -Identity site:Redmond

## 移除所有套用至網站範圍的用戶端版本原則

  - 此命令會移除所有在網站範圍所設定的用戶端版本原則：
    
        Get-CsClientVersionPolicy -Fiter "site:*" | Remove-CsClientVersionPolicy

## 移除不包含特定使用者代理程式的用戶端版本原則

  - 此命令會移除任何不包含 Windows Phone Lync (WPLync) 使用者代理程式規則的用戶端版本原則：
    
        Get-CsClientVersionPolicy | Where-Object {$_.Rules -notmatch "UserAgent=WPLync" | Remove-CsClientVersionPolicy

如需詳細資訊，請參閱＜[Remove-CsClientVersionPolicy](remove-csclientversionpolicy.md)＞ Cmdlet 說明主題。

