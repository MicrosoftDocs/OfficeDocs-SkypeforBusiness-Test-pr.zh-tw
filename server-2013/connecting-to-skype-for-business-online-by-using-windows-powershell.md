---
title: 使用 Windows PowerShell 連線至 Lync Online
TOCTitle: 使用 Windows PowerShell 連線至 Lync Online
ms:assetid: 6167dad9-9628-4fdb-bed1-bdb3f7108e64
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362795(v=OCS.15)
ms:contentKeyID: 56269097
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用 Windows PowerShell 連線至 Lync Online

 

_**上次修改主題的時間：** 2015-06-22_

安裝必要軟體後，即可開始使用 Windows PowerShell 管理 商務用 Skype Online。若要執行此操作，首先開啟 Windows PowerShell 的標準執行個體。您不需要開啟 Windows PowerShell 的特殊執行個體 (類似 Lync Server 管理命令介面 之類的情況)，也不需要開啟控制台應用程式或任何其他特殊類型的應用程式。這是因為 商務用 Skype Online 的管理作業是使用 Windows PowerShell 的遠端工作階段執行。這代表：

1.  您使用的是 Windows PowerShell 的一般工作階段連線至 商務用 Skype Online。進行遠端連線時，您是在您的本機電腦上操作且使用的是您的 Windows PowerShell 本機複本，但管理的是遠端系統上的物件 (即 商務用 Skype Online)。

2.  所有 Cmdlet、指令碼，以及管理 商務用 Skype Online 所需的其他項目均會下載至您的電腦。這些項目會保留在記憶體中，僅有在建立與 商務用 Skype Online 的遠端工作階段時才可供使用。請務必記住：當您遠端連線至 商務用 Skype Online 時，商務用 Skype Online Cmdlet (例如 [Get-CsTenant](get-cstenant.md)) 將會複製至您的電腦記憶體。在您的遠端工作階段中，您將能夠執行這些 Cmdlet。然而，這些 Cmdlet 僅提供於該遠端工作階段。例如，您可能會啟動第二個 Windows PowerShell 工作階段，但在此工作階段中並未連線至 商務用 Skype Online。若是嘗試從該工作階段中執行 **Get-CsTenant** Cmdlet，您將收到下列錯誤訊息：
    
        Get-CsTenant : The term 'Get-CsTenant' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
    
    另請注意，搜尋硬碟中的 **Get-CsTenant** Cmdlet (或任何其他 商務用 Skype Online Cmdlet) 將會出現空白。這是因為在您建立遠端工作階段時並未有任何項目實際儲存至您的硬碟。

3.  當您關閉遠端工作階段後，下載項目即會從電腦的記憶體中刪除。例如，您可能啟動 Windows PowerShell 遠端工作階段並執行 **Get-CsTenant** Cmdlet，然後關閉該工作階段。若是您重新啟動 Windows PowerShell，**Get-CsTenant** Cmdlet 將無法使用。若要存取 **Get-CsTenant** Cmdlet，您將需要重新連線至 商務用 Skype Online。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您正在使用混合式部署，應依照<a href="using-windows-powershell-in-a-hybrid-deployment-with-skype-for-business-online.md">在混合式部署中使用 Windows PowerShell</a> 中概述的步驟進行。</td>
</tr>
</tbody>
</table>


若要建立遠端連線連至 商務用 Skype Online，請先在本機電腦上啟動新的 Windows PowerShell 工作階段。如果您執行的是 Windows 7、Windows Server 2008 R2、Windows Server 2012 或 Windows Server 2012 R2，請執行下列操作：

  - 按一下 \[開始\]、\[所有程式\]、\[附屬應用程式\] 以及 \[Windows PowerShell\]，然後按一下 \[Windows PowerShell\]。

如果您執行的是 Windows 8 或 8.1，請改為執行下列操作：

  - 存取快速鍵列，按一下 \[搜尋\]，然後按一下 \[Windows PowerShell\]。若要在任何 Windows 8 或 8.1 電腦上快速存取快速鍵列 (無論是否為觸控螢幕)，請在按住 Windows 鍵的同時按下 C。

畫面出現 Windows PowerShell 主控台後，接著必須建立 Windows PowerShell 認證物件。認證物件可用於將您的使用者名稱與密碼安全地傳遞至 商務用 Skype Online。若要建立認證物件，請在 Windows PowerShell 命令提示字元中輸入下列命令，然後按 ENTER：

    $credential = Get-Credential

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在此範例中，您的使用者名稱與密碼將儲存於變數 $credential。您可以隨意命名該變數，只要遵循 Windows PowerShell 的變數名稱規則即可。然而，您必須使用特定變數才能儲存使用者名稱與密碼，否則您所建立的認證物件將會在建立後消失。</td>
</tr>
</tbody>
</table>


按下 ENTER 後，畫面應會出現 \[Windows PowerShell 認證\] 對話方塊：

![Windows PowerShell 登入認證](images/Dn362835.0f04e0a1-c9d6-4341-a0bb-ef721c4815fd(OCS.15).png "Windows PowerShell 登入認證")

在 \[使用者名稱\] 方塊中，輸入您的 商務用 Skype Online 使用者名稱。在 \[密碼\] 方塊中，輸入您的 商務用 Skype Online 密碼 (密碼將經過遮罩，不會顯示於畫面上)。例如，若是您的使用者名稱為 kenmyer@litwareinc.com 且密碼為 p@ssw0rd\!，對話方塊將會類似下列畫面：

![Windows PowerShell 認證登入](images/Dn362835.85977a0e-b14a-4aec-a45e-8548e9c9f691(OCS.15).png "Windows PowerShell 認證登入")

若要建立認證物件，請按一下 \[確定\]。若要確認物件是否建立完成，請直接在 Windows PowerShell 命令提示字元中輸入變數名稱，然後按下 ENTER：

    $credential

Windows PowerShell 將會顯示類似下列資訊作為回應：

    UserName                            Password
    --------                            --------
    kenmyer@litwareinc.com              System.Security.SecureString

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>請注意，<strong>Get-Credential</strong> Cmdlet 會接受您所輸入的任何認證而不會嘗試確認輸入的使用者名稱與密碼是否有效。確認作業僅會在您嘗試登入 商務用 Skype Online 時才會執行。</td>
</tr>
</tbody>
</table>


建立認證物件後，接著即可建立新的遠端 Windows PowerShell 工作階段來連線至 商務用 Skype Online。若要執行此操作，請在 Windows PowerShell 命令提示字元中輸入下列命令並按下 ENTER：

    $session = New-CsOnlineSession -Credential $credential

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>$session 是用於儲存資訊的變數，在此案例中，即為 商務用 Skype Online 連線的相關資訊。同樣地，您可以隨意為此變數命名，只要該名稱符合 Windows PowerShell 變數名稱準則 (例如，名稱不應包含空格或標點符號) 即可。</td>
</tr>
</tbody>
</table>


請確認您輸入的命令與所示命令完全相同 (變數名稱可能例外)。請注意，您的 商務用 Skype Online 網域名稱並不會造成任何影響；無論您的網域名稱為何，**New-CsOnlineSession** Cmdlet 均會將您連線至 Office 365，並且使用提供的認證將您登入。進行連線並通過驗證後，系統會根據您所提供的認證將您自動重新導向至適當的 URI。

若是連線成功，Windows PowerShell 主控台即會顯示類似下列訊息：

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

現在是否已可開始使用 Windows PowerShell 管理 商務用 Skype Online？答案是還沒。**New-CsOnlineSession** Cmdlet 會連線至 商務用 Skype Online 並且為您建立新工作階段。然而，您必須將新工作階段匯入至 Windows PowerShell 主控台。請執行下列命令以進行此操作：

    Import-PSSession $session

按下 ENTER 後，Windows PowerShell 主控台即會顯示類似下方的進度指示器：

    Creating implicit remoting module . . .
         Getting command information from remote session . . . 16 commands  
              received
         [oooooooooooooooo
         00:00:33 remaining

此時 Windows PowerShell 正在下載 Cmdlet 與其他管理 商務用 Skype Online 所需的項目。下載完成後，Windows PowerShell 主控台即會顯示類似以下資訊：

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enable-Cs ...}

此時即可準備開始使用 Windows PowerShell 管理 商務用 Skype Online。若要確認下載成功，並檢視可供使用的 商務用 Skype Online Cmdlet，首先必須判定包含所有 商務用 Skype Online Cmdlet 的暫時 Windows PowerShell 模組名稱。若要執行此操作，請從 Windows PowerShell 命令提示字元中執行下列命令：

    Get-Module

畫面將會出現類似以下資訊：

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

ModuleType 為 Script 的模組即為包含 商務用 Skype Online Cmdlet 的模組。若要傳回這類 Cmdlet 的清單，請以 Script 模組名稱執行 **Get-Command** Cmdlet：

    Get-Command -Module tmp_5astd3uh.m5v

接著 Windows PowerShell 應會顯示所有 商務用 Skype Online Cmdlet 的清單。

在您完成管理工作後，應一律執行下列命令後再關閉 Windows PowerShell 主控台：

    Remove-PSSession $session

**Remove-PSSession** Cmdlet 會將您從 商務用 Skype Online 中中斷並關閉遠端工作階段。事實上，若是您嘗試重新匯入工作階段 (透過執行 **Import-PSSession** Cmdlet)，您將會收到下列錯誤訊息：

    Import-PSSession : State of runspace is not valid for this operation.

該訊息只是代表為了重新連線至 商務用 Skype Online，您將需要建立新工作階段。

若是忘記在關閉 Windows PowerShell 主控台前移除工作階段 (或主控台非預期關閉)，並不會造成任何負面影響。在閒置 15 分鐘後，工作階段即會自行自動中斷。然而，根據預設，每個 商務用 Skype Online 系統管理員僅允許同時進行三個 商務用 Skype Online 連線。若是沒有移除工作階段即關閉 Windows PowerShell 主控台，關閉的工作階段仍將計為一個連線數，即使該連線目前並非使用中亦然。(且該連線將持續計為一個連線直至逾時。) 例如，您可能開啟並關閉 Windows PowerShell 主控台三次，每次都沒有移除 商務用 Skype Online 工作階段。在開啟 Windows PowerShell 並嘗試進行第四次連線時，您的命令將會沒有反應而無法連線。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若是 Windows PowerShell 在嘗試連線時呈現沒有反應的狀態，請按 Ctrl-C 以中斷停滯的命令。</td>
</tr>
</tbody>
</table>


雖然個別系統管理員僅可同時擁有三個 商務用 Skype Online 租用戶連線，但組織最多可同時擁有九個連線。這代表三名系統管理員可以各有三個連線，而九名系統管理員則各有一個 商務用 Skype Online 連線，依此類推。然而，沒有任何一名系統管理員可以有超過三個作用中的工作階段。

## 請參閱

#### 概念

[設定您的電腦以進行 Lync Online 管理](configuring-your-computer-for-skype-for-business-online-management.md)

