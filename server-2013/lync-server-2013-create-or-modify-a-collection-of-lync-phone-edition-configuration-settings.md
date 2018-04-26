---
title: 建立或修改 Lync Phone Edition 的組態設定集合
TOCTitle: 建立或修改 Lync Phone Edition 的組態設定集合
ms:assetid: 6cf714af-8f57-4a71-89ad-0a776302b2ba
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688086(v=OCS.15)
ms:contentKeyID: 49890107
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改 Lync Phone Edition 的組態設定集合

 

_**上次修改主題的時間：** 2013-02-23_

在安裝 Lync Server 時，您會得到 Lync Phone Edition 設定的全域集合，這些設定會套用至部署中所有執行 Lync Phone Edition 的裝置。您可以隨時變更這些設定，亦可建立新的設定集合，以套用至特定網站中的裝置。網站設定的優先順序高於全域設定。

組態設定包含集合名稱、範圍 (全域或網站)、SIP 安全性設定、記錄層次、語音服務品質 (QoS) 層級、電話鎖定設定與電話鎖定詳細資料，即 a) 個人識別碼 (PIN) 的解除鎖定時間必須為多久，以及 b) 電話自行鎖定前的閒置時間為多久。

## 建立 Lync Phone Edition 組態設定集合或編輯現有集合的設定

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[用戶端\]**，然後再按一下 **\[裝置組態\]** 導覽按鈕。

4.  在 **\[裝置組態\]** 頁面上，執行下列其中一項作業：
    
      - 若要建立新的 Lync Phone Edition 組態設定集合，請按一下 **\[新增\]**，選取一個網站，再按一下 **\[確定\]**檢視預設設定；若是需要，您也可以進行任何變更。
    
      - 若要在現有集合中編輯任何設定，請依序按一下集合、**\[編輯\]**功能表、**\[顯示詳細資料\]**，然後進行變更。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>若要返回以使用全域集合的預設設定，請依序按一下全域集合、<strong>[編輯]</strong>功能表、<strong>[刪除]</strong>，然後按一下 <strong>[確定]</strong>。這樣做並不會刪除全域集合，只是將設定重設為預設值。</td>
        </tr>
        </tbody>
        </table>


5.  按一下 **\[認可\]**。

## 使用 Lync Server 管理命令介面 Cmdlet 建立新的 Lync Phone Edition 組態設定

您也可以使用 Lync Server 管理命令介面與 **New-CsUCPhoneConfiguration** Cmdlet 來建立 Lync Phone Edition 組態設定 (僅限於網站範圍)。您可以從 Lync Server 2013 管理命令介面或 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 使用預設值建立新的 Lync Phone Edition 組態設定

  - 這個命令會針對 Redmond 網站建立一組新的 UC 電話組態設定：
    
        New-CsUCPhoneConfiguration -Identity "site:Redmond"
    
    由於以上的命令未指定任何參數 (強制的 Identity 參數除外)，新的組態設定集合將針對其所有屬性使用預設值。

## 在建立新的 Lync Phone Edition 組態設定時變更單一屬性值

  - 若要建立使用不同屬性質的設定，只需要加入適當的參數和參數值即可。例如，若要建立 UC 電話組態設定的集合，根據預設，需要執行電話鎖定，您可以使用下列命令：
    
        New-CsUCPhoneConfiguration -Identity "site:Redmond" -EnforcePhoneLock $True

## 在建立新的 Lync Phone Edition 組態設定時變更多項屬性值

  - 多項屬性值可透過加入多個參數加以修改。例如，這個命令會強制執行電話鎖定，也會將最小 PIN 長度限制設為 8 位數：
    
        New-CsUCPhoneConfiguration -Identity "site:Redmond" -EnforcePhoneLock $True -MinPhonePinLength 8

如需詳細資訊，請參閱 [New-CsUCPhoneConfiguration](new-csucphoneconfiguration.md)。

## 請參閱

#### 工作

[刪除現有的 Lync Phone Edition 組態設定集合](lync-server-2013-delete-an-existing-collection-of-lync-phone-edition-configuration-settings.md)  
[設定 Lync Phone Edition 的安全性設定](lync-server-2013-configure-security-settings-for-lync-phone-edition.md)  
[強制鎖定電話](lync-server-2013-enforce-phone-locking.md)

