---
title: 檢視 Lync Phone Edition 組態設定資訊
TOCTitle: 檢視 Lync Phone Edition 組態設定資訊
ms:assetid: 15f94478-651f-4063-9918-6a059f98df16
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687976(v=OCS.15)
ms:contentKeyID: 49889954
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視 Lync Phone Edition 組態設定資訊

 

_**上次修改主題的時間：** 2013-02-23_

您可以檢視執行 Lync Phone Edition 之裝置的組態資訊。此資訊會組織成集合。當您安裝 Lync Server 時，可以取得套用至部署中執行 Lync Phone Edition 之所有裝置的 Lync Phone Edition 設定集合。您也可以針對特定網站建立新的設定集合。網站設定的優先順序高於全域設定。每個設定集合都包含名稱、範圍 (全域或網站)、SIP 安全性設定、記錄層級、語音服務品質 (QoS) 層級、電話鎖定設定以及電話鎖定詳細資料 (也就是解除鎖定個人識別碼 (PIN) 的長度下限，以及電話自我鎖定之前的時間)。

## 檢視執行 Lync Phone Edition 之裝置的組態資訊

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[用戶端\]，然後按一下 \[裝置設定\] 導覽按鈕。

4.  在「裝置設定」頁面上，按一下您要檢視其相關資訊的設定集合。名稱、範圍、SIP 安全性設定、語音品質層級及電話鎖定設定會列示在主要頁面上。若要檢視記錄層級和電話鎖定詳細資料，請按一下 \[編輯\] 功能表，然後按一下 \[顯示詳細資料\]。

## 使用 Lync Server 管理命令介面 Cmdlet 來檢視 Lync Phone Edition 組態資訊

您也可以使用 Lync Server 管理命令介面和 **Get-CsUCPhoneConfiguration** Cmdlet 來檢視 Lync Phone Edition 組態設定。您可以從 Lync Server 2013 管理命令介面，或是從 Windows PowerShell 的遠端工作階段來執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視 Lync Phone Edition 組態資訊

  - 若要檢視所有 Lync Phone Edition 組態設定的相關資訊，請在 Lync Server 管理命令介面中輸入下列命令，然後按 ENTER 鍵。
    
        Get-CsUCPhoneConfiguration
    
    該命令會傳回如下資訊：
    
        Identity             : Global
        CalendarPollInterval : 00:03:00
        EnforcePhoneLock     : True
        PhoneLockTimeout     : 00:10:00
        MinPhonePinLength    : 6
        SIPSecurityMode      : High
        VoiceDiffServTag     : 40
        Voice8021p           : 0
        LoggingLevel         : Off

如需詳細資訊，請參閱＜[Get-CsUCPhoneConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUCPhoneConfiguration)＞。

## 請參閱

#### 工作

[建立或修改 Lync Phone Edition 的組態設定集合](lync-server-2013-create-or-modify-a-collection-of-lync-phone-edition-configuration-settings.md)  
[刪除現有的 Lync Phone Edition 組態設定集合](lync-server-2013-delete-an-existing-collection-of-lync-phone-edition-configuration-settings.md)  
[設定 Lync Phone Edition 的安全性設定](lync-server-2013-configure-security-settings-for-lync-phone-edition.md)  
[強制鎖定電話](lync-server-2013-enforce-phone-locking.md)

