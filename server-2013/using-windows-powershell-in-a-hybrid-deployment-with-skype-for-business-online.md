---
title: 在混合式部署中使用 Windows PowerShell
TOCTitle: 在混合式部署中使用 Windows PowerShell
ms:assetid: b19625d4-4b68-403c-a072-5296aa590556
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362835(v=OCS.15)
ms:contentKeyID: 56269141
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在混合式部署中使用 Windows PowerShell

 

_**上次修改主題的時間：** 2015-06-22_

在混合式部署中，組織會有部分使用者位於內部部署版本的 Lync Server 2013，而其他使用者位於 商務用 Skype Online。您可以使用單一的 Windows PowerShell 工作階段同時管理內部部署版本的 Lync Server 以及您的 商務用 Skype Online 租用戶。若要執行此操作，您將需要瞭解兩大事項：

1.  如何建立與 Lync Server 及 商務用 Skype Online 的同時連線。

2.  如何從同時連線參照 商務用 Skype Online 設定。

建立與 Lync Server 及 商務用 Skype Online 的同時連線超乎想像地簡單。若要執行此操作，首先依照正常方式連線 Lync Server：啟動 Lync Server 管理命令介面 或建立遠端連線連至前端集區。成功連線至內部部署版本的 Lync Server 後，接著採用在僅連線至 商務用 Skype Online 的相同程序連線至 商務用 Skype Online。若要建立此連線，首先必須使用您的 Office 365 登入資訊建立 Windows PowerShell 認證物件。若要執行此操作，請在 Windows PowerShell 命令提示字元中輸入下列內容，然後按下 ENTER：

    $credential = Get-Credential

按下 ENTER 後，您將會看到 \[Windows PowerShell 認證\] 對話方塊：

![Windows PowerShell 登入認證](images/Dn362835.0f04e0a1-c9d6-4341-a0bb-ef721c4815fd(OCS.15).png "Windows PowerShell 登入認證")

在 \[使用者名稱\] 方塊中，輸入您的 商務用 Skype Online 名稱。在 \[密碼\] 方塊中，輸入您的 商務用 Skype Online 密碼 (密碼將經過遮罩，不會顯示於畫面上)。例如，若是您的使用者名稱為 kenmyer@litwareinc.com 且密碼為 p@ssw0rd\!，對話方塊將會類似下列畫面：

![Windows PowerShell 認證登入](images/Dn362835.85977a0e-b14a-4aec-a45e-8548e9c9f691(OCS.15).png "Windows PowerShell 認證登入")

若要建立認證物件，請按一下 \[確定\]。建立認證物件後，即可執行下列命令以連線至 商務用 Skype Online：

    $session = New-CsOnlineSession -Credential $credential

請確認您精準輸入所示命令。請注意，無論您的 商務用 Skype Online 網域為何，都不會有任何影響。**New-CsOnlineSession** Cmdlet 均會將您連線至 Office 365 並使用所提供的認證將您登入。在您進行連線並通過驗證後，系統會將您自動重新導向至適當的 URI。

若是連線成功，您將會在 Windows PowerShell 主控台中看到類似下列訊息：

    VERBOSE: Determining domain to admin
    VERBOSE: AdminDomain = litwareinc.com
    VERBOSE: Discovering PowerShell endpoint URI
    VERBOSE: TargetUri = https://webdir0d.litwareinc.com/OcsPowerShellLiveId
    VERBOSE: Requesting authentication token
    VERBOSE: Success
    VERBOSE: Initializing remote session
    VERBOSE: Success
    Id Name       ComputerName    State        ConfigurationName     Availability -- ----       ------------    -----        -----------------     ------------
    2 Session2    litwarein...    Opened       Microsoft.PowerShell  Available

成功建立與 商務用 Skype Online 的連線後，執行類似如下命令以匯入該工作階段：

    Import-PSSession $session -AllowClobber

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>AllowClobber 參數可確保所有 商務用 Skype Online Cmdlet 均已匯入，包括與一般的 Lync Server Cmdlet 具有相同名稱的 Cmdlet。這些 Cmdlet 為數眾多，因為大部分 商務用 Skype Online Cmdlet，包括 <a href="get-csmeetingconfiguration.md">Get-CsMeetingConfiguration</a>、<a href="new-csexumcontact.md">New-CsExUmContact</a>、<a href="remove-csvoicepolicy.md">Remove-CsVoicePolicy</a> 等均有內部部署的對等項目。成對的 Cmdlet (例如 Lync Server<strong>Get-CsMeetingConfiguration</strong> Cmdlet 與 商務用 Skype Online<strong>Get-CsMeetingConfiguration</strong> Cmdlet) 兩者相同：使用哪個 Cmdlet 並無任何差別。使用 AllowClobber 參數的唯一理由是要防止您的畫面出現警告訊息。</td>
</tr>
</tbody>
</table>


此時，您已可以開始管理內部部署版本的 Lync Server 與 商務用 Skype Online。這時候，您可能也會有個重要的疑問：如何區別 Lync Server 原則與設定以及 商務用 Skype Online 原則與設定？例如，您可能會想要變更全域會議組態設定。為執行此操作，您會執行下列命令：

    Set-CsMeetingConfiguration -Identity "global" -AdmitAnonymousUsersByDefault $False

此命令會修改全域設定；但是是修改哪些全域設定？是 Lync Server 內部部署？還是 商務用 Skype Online？是兩者皆是？還是兩者皆否？

在這個特殊案例中，內部部署設定將會進行修改。如何得知呢？因為 Tenant 參數並未包含在命令中。若是您同時連線至 Lync Server 內部部署與 商務用 Skype Online，則除非另有指示，否則可在任一平台上運作的 Cmdlet 將於 Lync Server 上執行。若要指示 Cmdlet 於另一個平台上執行，唯一的方法是在執行命令時加上 Tenant 參數。例如，下列命令會更新租用戶識別碼為 bf19b7db-6960-41e5-a139-2aa373474354 之 商務用 Skype Online 租用戶的全域設定：

    Set-CsMeetingConfiguration -Identity "global" -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AdmitAnonymousUsersByDefault $False

Tenant 參數是其中的關鍵。下列命令會傳回 Lync Server 內部部署的全域外部存取原則：

    Get-CsExternalAccessPolicy -Identity "global"

而下列命令會傳回 商務用 Skype Online 租用戶的全域外部存取原則：

    Get-CsExternalAccessPolicy -Identity "global" -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

請記住，有超過 700 個內部部署的 Cmdlet。然而，大部分的 Cmdlet 並無 Tenant 參數，代表這些 Cmdlet 無法用於 商務用 Skype Online。另請注意，有部分 Cmdlet 具有 Tenant 參數，但還無法用於 商務用 Skype Online。若要擷取可用於 商務用 Skype Online 的確切 Cmdlet，請透過 Windows PowerShell 命令提示字元執行下列命令：

    Get-Module

畫面將會出現類似以下資訊：

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

ModuleType 為 Script 的模組為包含 商務用 Skype Online Cmdlet 的模組。若要傳回該類 Cmdlet 的清單，請以 Script 為模組名稱執行 **Get-Command** Cmdlet：

    Get-Command -Module tmp_5astd3uh.m5v

Windows PowerShell 將會顯示所有 商務用 Skype Online Cmdlet 的清單。

**疑難排解混合部署中的連線問題**

有時候，系統管理員登入 Office 365 時，若是使用內部部署帳戶 (例如 administrator@litwareinc.net)，而不是使用 Office 365 帳戶 (例如 administrator@litwareinc.onmicrosoft.com) ，可能會發生問題。若目錄同步處理順利運作，則您應該可使用這兩種帳戶登入。這是混合部署的優點之一。然而，系統管理員有時候仍然無法使用其內部部署帳戶登入。這通常是因為自動探索會將登入指向 Lync Server 的內部部署安裝，而不是 Office 365。

幸運的是，有個簡單的方法可解決這個問題。使用 **New-CsOnlineSession** Cmdlet 登入 Office 365 時，只需包括 OverrideAdminDomain 參數並在其後加上 Office 365 網域名稱即可。例如，若要使用 administrator@litwareinc.net 帳戶登入 Office 365，請包括 OverrideAdminDomain 參數，並在其後加上網域名稱 litwareinc.onmicrosoft.com：

    $session = New-CsOnlineSession -Credential $credential -OverrideAdminDomain "litwareinc.onmicrosoft.com"

該命令會明確地將登入嘗試指向 Office 365 伺服器與 litwareinc.onmicrosoft.com 網域。

