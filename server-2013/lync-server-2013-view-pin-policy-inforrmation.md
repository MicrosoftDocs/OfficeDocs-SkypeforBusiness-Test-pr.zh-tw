---
title: 檢視 PIN 原則資訊
TOCTitle: 檢視 PIN 原則資訊
ms:assetid: 1d48b060-d77f-44ee-b70f-3ce128aedac4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687985(v=OCS.15)
ms:contentKeyID: 49889966
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視 PIN 原則資訊

 

_**上次修改主題的時間：** 2013-02-23_

您可以使用 \[PIN 原則\] 索引標籤，檢視透過 IP 電話連線至 Lync 2013 的使用者個人識別碼 (PIN) 驗證。若要使用 PIN 驗證，請確定已在 Web 服務設定中選取了 \[啟用 PIN 驗證\]。如需詳細資訊，請參閱＜[修改現有 Web 服務組態設定](lync-server-2013-modify-existing-web-service-configuration-settings.md)＞。

請遵循下列步驟來修改使用者層級或網站層級的 PIN 原則。

## 若要檢視 Lync Server 控制台中的 PIN 原則相關資訊

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 \[安全性\] 和 \[PIN 原則\]。

4.  在「PIN 原則」 頁面上，依序按一下原則、\[編輯\] 和 \[顯示詳細資料\]。

## 使用 Lync Server PowerShell Cmdlet 來檢視 PIN 原則

您也可以使用 Windows PowerShell 和 Get-CsPinPolicy Cmdlet 來檢視 PIN 原則。此 Cmdlet 可從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視 PIN 原則

  - 若要檢視 PIN 原則的相關資訊，請在 Lync Server 管理命令介面中輸入下列命令，然後按 ENTER 鍵：
    
        Get-CsPinPolicy
    
    這會傳回類似如下的資訊：
    
        Identity             : Global
        Description          :
        MinPasswordLength    : 5
        PINHistoryCount      : 0
        AllowCommonPatterns  : False
        PINLifetime          : 0
        MaximumLogonAttempts :

如需詳細資訊，請參閱＜[Get-CsPinPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsPinPolicy)＞Cmdlet 的說明主題。

## 請參閱

#### 工作

[修改現有 Web 服務組態設定](lync-server-2013-modify-existing-web-service-configuration-settings.md)  
[建立新 PIN 原則](lync-server-2013-create-a-new-pin-policy.md)

