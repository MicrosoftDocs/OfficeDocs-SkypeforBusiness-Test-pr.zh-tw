---
title: 設定 Lync Phone Edition 的安全性設定
TOCTitle: 設定 Lync Phone Edition 的安全性設定
ms:assetid: 6e7cec17-8a79-4428-9300-8821256c46cf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg521014(v=OCS.15)
ms:contentKeyID: 49291243
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Lync Phone Edition 的安全性設定

 

_**上次修改主題的時間：** 2013-02-23_

透過您的 SIP 安全性設定及電話鎖定設定以改善執行 Lync Phone Edition 之裝置的安全性。

## 設定 Lync Phone Edition 的安全性設定

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[用戶端\]** 和 **\[裝置設定\]**。

4.  在 **\[裝置設定\]** 頁面的裝置設定清單中，按兩下想要變更其安全性設定的設定。

5.  在 **\[編輯裝置設定\]** 的 **\[SIP 安全性\]**中指定 SIP 安全性等級。建議您使用 **\[高\]** 預設等級。

6.  在 **\[編輯裝置設定\]** 的 **\[電話鎖定\]**下方，請選取或清除 **\[強制執行裝置鎖定\]** 核取方塊 (預設選取)，並指定最小 PIN 長度限制 (預設為 6 個字元) 和逾時期限 (預設為 10 分鐘)。建議您使用這些預設值或增加 PIN 長度及/或縮短逾時期限。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如需詳細資訊，請參閱＜<a href="lync-server-2013-enforce-phone-locking.md">強制鎖定電話</a>＞。</td>
    </tr>
    </tbody>
    </table>


## 使用 Lync Server 管理命令介面 Cmdlet 設定 Lync Phone Edition 電話的安全性設定

您也可使用 Lync Server 管理命令介面與 **Get-CsUCPhoneConfiguration** Cmdlet 來管理安全性設定。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 修改 SIP 安全性模式

  - 這個命令會將 UC 電話設定全域集合的 SIPSecurityMode 設為 Medium，亦會將 SIP 安全性設為 Low 或 High (預設值)。
    
        Set-CsUCPhoneConfiguration -Identity global -SIPSecurityMode "Medium"

## 修改最小 PIN 長度

  - 在此範例中，所有 UC 電話設定皆將最小 PIN 長度限制修改為 7 位數。
    
        Get-CsUCPhoneConfiguration | Set-CsUCPhoneConfiguration -MinPhonePinLength 7

如需詳細資訊，請參閱 [Get-CsUCPhoneConfiguration](get-csucphoneconfiguration.md)。

## 請參閱

#### 概念

[管理 Lync Server 2013 授權](lync-server-2013-managing-lync-server-authentication.md)  

#### 其他資源

[在 Lync Server 2013 中管理裝置、電話及用戶端應用程式](lync-server-2013-managing-devices-phones-and-client-applications.md)

