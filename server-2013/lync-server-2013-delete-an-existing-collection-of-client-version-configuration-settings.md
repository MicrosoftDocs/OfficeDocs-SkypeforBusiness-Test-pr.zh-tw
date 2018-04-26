---
title: 刪除現有的用戶端版本組態設定集合
TOCTitle: 刪除現有的用戶端版本組態設定集合
ms:assetid: 70bf1216-d0d2-45ce-881f-b8edadf3cec7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ898480(v=OCS.15)
ms:contentKeyID: 52056129
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除現有的用戶端版本組態設定集合

 

_**上次修改主題的時間：** 2013-02-23_

如果您想移除先前對網站設定的用戶端組態設定，可以從 Lync Server 2013 控制台或 Lync Server 2013 管理命令介面移除設定。

## 使用 Lync Server 控制台移除用戶端組態設定

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列，按一下 \[用戶端\]，然後按一下 \[用戶端版本設定\] 導覽按鈕。

4.  選取網站，依序按一下 \[編輯\]、\[刪除\]，然後按一下 \[確定\]。

## 使用 Windows PowerShell Cmdlet 移除用戶端版本組態設定

您可以使用 **Remove-CsClientVersionConfiguration** Cmdlet 來刪除用戶端版本組態設定。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 移除用戶端版本組態設定的特定集合

  - 下列命令會移除已套用至 Redmond 網站的用戶端版本組態設定：
    
        Remove-CsClientVersionConfiguration -Identity "site:Redmond"

## 移除套用至網站範圍的所有用戶端版本組態設定

  - 此命令會移除在網站範圍中設定的所有用戶端版本組態設定：
    
        Get-CsClientVersionConfiguration -Filter site:* | Remove-CsClientVersionConfiguration

## 根據 DefaultAction 屬性值移除所有用戶端版本組態設定

  - 此命令會移除預設動作已設為 "Block" 的所有用戶端版本組態設定：
    
        Get-CsClientVersionConfiguration | Where-Object {$_.DefaultAction -eq "Block" | Remove-CsClientVersionConfiguration

如需詳細資訊，請參閱＜[Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md)＞ Cmdlet 的說明主題。

