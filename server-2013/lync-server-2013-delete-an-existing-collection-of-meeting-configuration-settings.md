---
title: 刪除現有的會議組態設定集合
TOCTitle: 刪除現有的會議組態設定集合
ms:assetid: 92ff8a91-05c5-4047-a533-5dff12f22299
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688136(v=OCS.15)
ms:contentKeyID: 49890210
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除現有的會議組態設定集合

 

_**上次修改主題的時間：** 2013-02-23_

您可以刪除網站或使用者設定。全域設定無法移除。如果您刪除全域設定，即會將全域設定自動重設為預設值。

## 刪除網站或使用者會議設定

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[會議\]，然後按一下 \[會議設定\]。

4.  在會議設定清單中，依序按一下要刪除的網站或集區設定、\[編輯\] 及 \[刪除\]。

## 使用 Lync Server PowerShell Cmdlet 移除會議組態設定

會議設定也可以使用 Windows PowerShell 和 Remove-CsMeetingConfiguration Cmdlet 來刪除。此 Cmdlet 可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 移除指定的會議組態設定集合

  - 此命令會移除套用至 Redmond 網站的會議組態設定：
    
        Remove-CsMeetingConfiguration -Identity "site:Redmond"

## 移除所有套用至網站範圍的會議組態設定

  - 此命令會移除所有套用至網站範圍的會議組態設定：
    
        Get-CsMeetingConfiguration -Filter "site:*" | Remove-CsMeetingConfiguration

## 移除所有預設允許匿名使用者的會議組態設定

  - 此外，這一個選項也會移除所有預設允許匿名使用者加入的設定：
    
        Get-CsMeetingConfiguration | Where-Object {$_.AdmitAnonymousUsersByDefault -eq $True} | Remove-CsMeetingConfiguration

如需詳細資訊，請參閱適用於 [Remove-CsMeetingConfiguration](remove-csmeetingconfiguration.md) Cmdlet 的說明主題。

