---
title: 檢視用戶端版本原則規則
TOCTitle: 檢視用戶端版本原則規則
ms:assetid: f3a0215f-f72f-4e9b-a07b-25858dc4203a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ923060(v=OCS.15)
ms:contentKeyID: 52056254
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視用戶端版本原則規則

 

_**上次修改主題的時間：** 2013-02-23_

用戶端版本原則由一組用戶端版本原則規則所組成。這些規則定義使用者嘗試透過特定用戶端與用戶端版本登入時所須執行的動作。您可以從Lync Server 2013 控制台或Lync Server 2013 管理命令介面檢視用戶端版本原則規則。

## 使用 Lync Server 控制台檢視用戶端版本原則規則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列，按一下 \[用戶端\]，然後按一下 \[用戶端版本原則\] 導覽按鈕。

4.  在「用戶端版本原則」頁面，按兩下您要檢視的用戶端版本原則。

5.  規則隨即顯示於「編輯用戶端版本原則」頁面。若要檢視某項規則的詳細資訊，請選取該項規則，然後按一下 \[顯示詳細內容\]。

## 使用 Windows PowerShell Cmdlet 檢視用戶端版本原則規則

您可以使用 Lync Server 管理命令介面和 **Get-CsClientVersionPolicyRule** Cmdlet 檢視用戶端版本原則規則。此 Cmdlet 可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視用戶端版本原則規則

  - 若要檢視用戶端版本原則規則，請在 Lync Server 管理命令介面中輸入下列命令，然後按 ENTER：
    
        Get-CsClientVersionPolicyRule
    
    將針對每個設定的規則傳回類似如下的資訊：
    
        Identity          : Global/2336c611-a243-4c5d-994b-eea8a524d0e4
        Priority          : 0
        RuleId            : 2336c611-a243-4c5d-994b-eea8a524d0e4
        Description       :
        Action            : Block
        ActionUrl         :
        MajorVersion      : 1
        MinorVersion      : 3
        BuildNumber       :
        QfeNumber         :
        UserAgent         : RTC
        UserAgentFullName :
        Enabled           : True
        CompareOp         : LEQ

如需詳細資訊，請參閱 [Get-CsClientVersionPolicyRule](get-csclientversionpolicyrule.md) Cmdlet 的說明主題。

