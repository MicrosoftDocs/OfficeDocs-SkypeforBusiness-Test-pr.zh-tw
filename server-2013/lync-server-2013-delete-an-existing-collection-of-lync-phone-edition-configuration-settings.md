---
title: 刪除現有的 Lync Phone Edition 組態設定集合
TOCTitle: 刪除現有的 Lync Phone Edition 組態設定集合
ms:assetid: 1bfc427d-4dcd-4199-b25f-8d5cfec2164f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687984(v=OCS.15)
ms:contentKeyID: 49889965
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除現有的 Lync Phone Edition 組態設定集合

 

_**上次修改主題的時間：** 2013-02-23_

若您不再需要使用執行 Lync Phone Edition 之裝置的設定集合，請將其刪除。若您刪除網站的集合，該網站中的電話就會套用全域設定。您無法刪除全域集合。

> [!NOTE]  
> 若您不想刪除集合，而只想變更部分設定。如需如何進行這項作業的詳細資訊，請參閱＜<a href="lync-server-2013-create-or-modify-a-collection-of-lync-phone-edition-configuration-settings.md">建立或修改 Lync Phone Edition 的組態設定集合</a>＞。



## 若要刪除 Lync Phone Edition 組態設定

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[用戶端\]，然後按一下 \[裝置設定\] 導覽按鈕。

4.  在「裝置設定」 頁面中，按一下欲刪除的集合，然後按一下 \[編輯\] 功能表，再按一下 \[刪除\]。
    
    > [!NOTE]  
    > 若您要刪除全域集合，設定就會還原為預設值，但集合仍會存在。
    


5.  在確認對話方塊中，按一下 \[確定\]。

## 若要使用 Lync Server 管理命令介面 Cmdlet 來移除 Lync Phone Edition 組態設定

您可使用 Windows PowerShell 和 **Remove-CsUCConfiguration** Cmdlet 來移除 Lync Phone Edition 組態設定。您可從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段來執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 若要移除特定的 Lync Phone Edition 組態設定集合

  - 此命令會刪除套用至 Redmond 網站的 UC 電話組態設定：
    
        Remove-CsUCPhoneConfiguration -Identity "site:Redmond"

## 若要移除套用至網站範圍的所有 Lync Phone Edition 組態設定

  - 此命令會移除套用至服務範圍的所有 UC 電話組態設定：
    
        Get-CsUCPhoneConfiguration -Filter "site:*" | Remove-CsUCPhoneConfiguration

## 若要移除已停用電話鎖定的所有 Lync Phone Edition 組態設定

  - 此命令可刪除已停用電話鎖定的任何 UC 電話組態設定集合：
    
        Get-CsUCPhoneConfiguration | Where-Object {$_.EnforcePhoneLock -eq $False} | Remove-CsUCPhoneConfiguration

如需詳細資訊，請參閱＜[Remove-CsUCPhoneConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsUCPhoneConfiguration)＞。

