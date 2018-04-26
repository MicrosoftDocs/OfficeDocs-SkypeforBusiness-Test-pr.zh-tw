---
title: 強制鎖定電話
TOCTitle: 強制鎖定電話
ms:assetid: 1f89298b-aea9-4952-93ca-0270b565792b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520963(v=OCS.15)
ms:contentKeyID: 49290299
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 強制鎖定電話

 

_**上次修改主題的時間：** 2013-02-23_

Lync Phone Edition 裝置可為了安全目的加以鎖定。若您強制執行電話鎖定，則執行 Lync Phone Edition 的裝置會在您設定的一段時間之後進行鎖定。電話鎖定時，使用者仍可撥打電話，但無法存取行事曆和連絡人資訊、語音信箱及通話記錄，也無法使用搜尋。使用者必須輸入 PIN 才能將電話解除鎖定。

若要強制執行電話鎖定，可使用 Lync Server 控制台或 Lync Server PowerShell Cmdlet 加以啟用及設定。您可以強制執行全域電話鎖定或只限於所設定的網站之內。

## 設定並強制執行電話鎖定

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  依序按一下 **\[用戶端\]** 和 **\[裝置設定\]**。

4.  在 **\[裝置設定\]** 索引標籤的裝置設定清單中，按兩下您要變更電話鎖定設定的設定。

5.  在 **\[編輯裝置設定\]** 對話方塊中，確認已選取 **\[強制執行裝置鎖定\]** 核取方塊。

6.  在 \[最小 PIN 長度\] 中，接受解除鎖定 PIN 必須包含之最少位數的預設值，或指定新的值。PIN 長度的範圍為 4 至 15 位數，預設長度為 6 位數。

7.  在 \[電話鎖定逾時\] 中，接受電話自行鎖定前需經過之最小時間長度的預設值，或指定新的值。逾時範圍是 0 到 60 分鐘，預設值是 10 分鐘。請以 HH:MM:SS 格式輸入此值。

8.  按一下 **\[認可\]**。

## 使用 Windows PowerShell Cmdlet 來強制執行電話鎖定

您可以使用 Set-CsUCPhoneConfiguration Cmdlet 來強制執行電話鎖定，此 Cmdlet 可從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 啟用電話鎖定

  - 下列命令可啟用 Redmond 網站的電話鎖定。若要停用電話鎖定，請將 EnforcePhoneLock 屬性設為 ($False)。
    
        Set-CsUCPhoneConfiguration -Identity" site:Redmond" -EnforcePhoneLock $True

## 啟用電話鎖定並修改電話鎖定逾時

  - 此命令可啟用電話鎖定，也可將電話鎖定逾時設為 30 分鐘。
    
        Set-CsUCPhoneConfiguration -Identity" site:Redmond" -EnforcePhoneLock $True -PhoneLockTimeout "00:30:00"

## 啟用全組織電話鎖定

  - 在此範例中，組織中所使用的所有 UC 電話組態設定都啟用了電話鎖定。
    
        Get-CsUCPhoneConfiguration | Set-CsUCPhoneConfiguration  -EnforcePhoneLock $True

如需詳細資訊，請參閱＜[Set-CsUCPhoneConfiguration](set-csucphoneconfiguration.md)＞Cmdlet 的說明主題。

## 請參閱

#### 概念

[管理 Lync Server 2013 授權](lync-server-2013-managing-lync-server-authentication.md)  

#### 其他資源

[在 Lync Server 2013 中管理裝置、電話及用戶端應用程式](lync-server-2013-managing-devices-phones-and-client-applications.md)

