---
title: 指派每位使用者的語音原則
TOCTitle: 指派每位使用者的語音原則
ms:assetid: 9ee47ee7-1030-43b8-a4dc-bf685ea24659
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688155(v=OCS.15)
ms:contentKeyID: 49890231
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 指派每位使用者的語音原則

 

_**上次修改主題的時間：** 2013-02-22_

全域與網站層級的語音原則會自動指派給所有啟用 Enterprise Voice 的 Lync Server 2013 使用者帳戶。您也可以使用 Lync Server 2013 控制台或 Lync Server 2013 管理命令介面來指派語音原則給特定使用者。請使用本主題中的程序，明確將個別使用者的原則指派給 Lync Server 使用者。

## 使用 Lync Server 控制台指派使用者專屬的語音原則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[使用者\]，然後搜尋想要設定的使用者帳戶。

4.  在列出搜尋結果的表格中，依序按一下使用者帳戶、\[編輯\] 及 \[顯示詳細資料\]。

5.  在 \[語音原則\] 底下的 \[編輯 Lync Server 使用者\] 中，選取想要套用的使用者原則。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>[&lt;自動&gt;] 設定會套用預設伺服器或全域原則設定。</td>
    </tr>
    </tbody>
    </table>


## 使用 Lync Server 管理命令介面指派使用者專屬的語音原則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  若要將現有的使用者語音原則指派給使用者，請在命令提示字元中執行下列命令：
    
        Grant-CsVoicePolicy -Identity <UserIdParameter> -PolicyName <String>
    
    例如：
    
        Grant-CsVoicePolicy -Identity "Bob Kelly" -PolicyName VoicePolicyJapan
    
    在此範例中，會指派名稱為 **VoicePolicyJapan** 的語音原則給顯示名稱為 Bob Kelly 的使用者。

如需關於指派使用者專屬語音原則或執行 **Grant-CsVoicePolicy** Cmdlet 的詳細資訊，請參閱 [Lync Server 管理命令介面](lync-server-2013-lync-server-management-shell.md)文件。

## 使用 Windows PowerShell Cmdlet 指派個別使用者的語音原則

您也可以使用 Windows PowerShell 和 **Grant-CsVoicePolicy** Cmdlet 來指派個別使用者的語音原則。此 Cmdlet 可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 指派個別使用者的語音原則給單一使用者

  - 下列命令會將個別使用者的語音原則 RedmondVoicePolicy 指派給使用者 Ken Myer。
    
        Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "RedmondVoicePolicy"

## 將個別使用者的語音原則指派給多個使用者

  - 此命令會將個別使用者的語音原則 FinanceVoicePolicy 指派給所有在 Active Directory 的 Finance OU 中具有帳戶的使用者。如需關於此命令中所使用之 OU 參數的詳細資訊，請參閱 [Get-CsUser](get-csuser.md) Cmdlet 的文件。
    
        Get-CsUser -OU "ou=Finance,ou=North America,dc=litwareinc,dc=com" | Grant-CsVoicePolicy -PolicyName "FinanceVoicePolicy"

## 取消指派個別使用者的語音原則

  - 下列命令會取消指派先前指派給 Ken Myer 的個別使用者語音原則。取消指派個別使用者語音原則之後，系統會自動使用全域原則來管理 Ken Myer，或者如果有本機網站原則，則會使用本機網站原則來管理。網站原則的優先順序高於全域原則。
    
        Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName $Null

如需詳細資訊，請參閱 [Grant-CsVoicePolicy](grant-csvoicepolicy.md) Cmdlet 的說明主題。

## 請參閱

#### 工作

[停用 Enterprise Voice 的使用者](lync-server-2013-disable-a-user-for-enterprise-voice.md)  

#### 其他資源

[Lync Server 管理命令介面](lync-server-2013-lync-server-management-shell.md)

