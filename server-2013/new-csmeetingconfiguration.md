---
title: New-CsMeetingConfiguration
TOCTitle: New-CsMeetingConfiguration
ms:assetid: 0043c9e7-83c6-4f07-88d2-7018c65c1654
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398065(v=OCS.15)
ms:contentKeyID: 49289886
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsMeetingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

在網站或服務範圍建立新的會議組態設定集合。會議組態設定可用於指定使用者所能建立的會議類型，以及控制匿名使用者和電話撥入式會議使用者如何 (或能否) 加入這些會議。請注意，這些設定只會影響排程會議，而不會影響在 Lync 中按一下 \[立即開會\] 選項所建立的臨時會議。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsMeetingConfiguration -Identity <XdsIdentity> [-AdmitAnonymousUsersByDefault <$true | $false>] [-AssignedConferenceTypeByDefault <$true | $false>] [-Confirm [<SwitchParameter>]] [-CustomFooterText <String>] [-DesignateAsPresenter <None | Company | Everyone>] [-EnableAssignedConferenceType <$true | $false>] [-Force <SwitchParameter>] [-HelpURL <String>] [-InMemory <SwitchParameter>] [-LegalURL <String>] [-LogoURL <String>] [-PstnCallersBypassLobby <$true | $false>] [-RequireRoomSystemsAuthorization <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會針對 Redmond 網站 (-Identity site:Redmond)，建立新的會議組態設定集合。除了指定 Identity 之外，此命令還可以加入三個選用的參數：EnableAssignedConferenceType、AssignedConferenceTypeByDefault 和 AdmitAnonymousUsersByDefault。在所有三種情況下，這些參數都設為 False。這表示公開會議類型將會停用；預設會議類型將不會設為公開會議；而預設將不准許匿名使用者加入會議。

請注意，如果 Identity 為 site:Redmond 的會議組態設定集合已經存在，此命令將會失敗。那是因為一個指定網站最多只能套用一個會議組態設定集合。

    New-CsMeetingConfiguration -Identity site:Redmond -EnableAssignedConferenceType $False -AssignedConferenceTypeByDefault $False -AdmitAnonymousUsersByDefault $False

## 範例 2

範例 2 會針對 Redmond 網站，示範一個建立新會議組態設定集合的替代方式；在此範例中，這些設定一開始只會在記憶體中建立，而且只會在稍後套用至網站。為達成此目的，範例中的第一個命令會使用 **New-CsMeetingConfiguration** Cmdlet 為 Redmond 網站建立新的會議設定。命令尾端加上 InMemory 參數，以確保這些新的設定只在記憶體中建立，而不立即套用至 Redmond 網站。(由於這些設定僅存在於記憶體中，因此必須儲存在變數中。在此範例中會儲存在名為 $x 的變數中)。

建立這些虛擬會議設定後，命令 2、3 及 4 用於修改這些設定的屬性 (EnableAssignedConferenceType、AssignedConferenceTypeByDefault 以及 AdmitAnonymousUsersByDefault)。在最後一個命令中， **Set-CsMeetingConfiguration** Cmdlet 搭配 Instance 參數會用於實際將虛擬設定套用至 Redmond 網站。請注意，這個最終的步驟相當重要：如果您沒有呼叫 **Set-CsMeetingConfiguration** Cmdlet，新會議組態設定將永遠不會套用至 Redmond 網站。而您的虛擬設定會在結束 Windows PowerShell 工作階段或刪除變數 $x 後消失。

    $x = New-CsMeetingConfiguration -Identity site:Redmond -InMemory
    $x.EnableAssignedConferenceType = $False 
    $x.AssignedConferenceTypeByDefault = $False 
    $x.AdmitAnonymousUsersByDefault = $False
    Set-CsMeetingConfiguration -Instance $x

## 詳細描述

會議是 Lync Server 不可或缺的一部分。 **CsMeetingConfiguration** Cmdlet 可讓系統管理員控制使用者可以建立的會議類型，並決定會議處理匿名使用者與電話撥入式會議使用者的方式。例如，您可以設定會議，以便自動准許透過公用交換電話網路 (PSTN) 撥入的任何人加入會議。或者，您也可以設定會議，不自動允許電話撥入式使用者加入會議，而是送往會議大廳。這些電話撥入式使用者會一直停留在大廳，直到主持人准許他們加入會議為止。

如前所述，這些設定只會影響排程會議，而不會影響在 Microsoft Lync 中按一下 \[立即開會\] 所建立的臨時會議。當您按一下 \[立即開會\] 建立會議時，會自動開啟所有人的參與者存取權，且匿名使用者可以加入會議，而不需要在大廳中等候。不論您如何使用 CsMeetingConfiguration Cmdlet 設定會議設定，都會發生此情況。

**New-CsMeetingConfiguration** Cmdlet 可讓您在網站或服務範圍 (儘管只針對 User Services) 建立新會議組態集合。您無法在全域範圍建立會議設定，因為已經有全域的會議設定集合。

請注意，每個網站或服務最多只能夠有一個會議組態設定集合。如果您嘗試為 Redmond 網站建立新的設定，而 Redmond 網站已經有一個會議組態設定集合，則您的命令將會失敗。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsMeetingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsMeetingConfiguration"}

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>新會議組態設定集合的唯一識別碼。您只能在網站或服務範圍建立會議組態設定。若要在網站範圍建立新的設定，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。若要在服務範圍建立新的設定，請使用類似下列的語法：-Identity &quot;service:UserServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>請注意，如果指定的網站或服務已經有會議組態設定集合， <strong>New-CsMeetingConfiguration</strong> Cmdlet 呼叫就會失敗。</p></td>
</tr>
<tr class="even">
<td><p><em>AdmitAnonymousUsersByDefault</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定會議預設是否允許匿名使用者 (亦即，未驗證的使用者) 出席。如果您想讓新的會議預設允許匿名使用者參與，請將此值設為 True。如果您希望新的會議預設不允許匿名使用者參與，請將此值設為 False。預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>AssignedConferenceTypeByDefault</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定預設是否將新的會議設作公開會議。將此值設為 True，則預設會使用公開會議；將此值設為 False，則預設會使用私人會議。預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>CustomFooterText</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要用在自訂會議邀請函上的文字。</p></td>
</tr>
<tr class="even">
<td><p><em>DesignateAsPresenter</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.DesignateAsPresenter</p></td>
<td><p>表示當使用者加入會議時，自動指定哪些使用者為主持人 (除了會議召集人)。有效的選擇如下：None、Company 以及 Everyone。根據預設，DesignateAsPresenter 會設為 Company，表示組織中的每個人在加入會議當時就具有主持人權限。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableAssignedConferenceType</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否允許使用者排程公開會議。在公開會議中，每次舉行會議時，會議識別碼和會議連結會保持一致。在私人會議中，會議識別碼和會議連結會隨著會議而有所不同。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>HelpURL</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可協助使用者參加會議的網站 URL。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>LegalURL</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>含有法律資訊及會議免責聲明的網站 URL。</p></td>
</tr>
<tr class="even">
<td><p><em>LogoURL</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要用在自訂會議邀請函上的影像 URL。</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnCallersBypassLobby</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否應自動允許以公用交換電話網路 (PSTN) 電話線路撥進的使用者加入會議。如果設為 True，PSTN 來電者會自動獲准加入會議。如果設為 False，則 PSTN 來電者會在一開始便被轉到會議大廳。在此情況下，他們必須置於保留狀態，直到會議主持人授與其存取會議的權限為止。預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>RequireRoomSystemsAuthorization</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True ($True) 時，所有使用者都必須先經過驗證，才能使用 Lync Room System 來參加會議。預設值為 False ($False)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要建立新會議組態設定的 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **New-CsMeetingConfiguration** Cmdlet 不接受管線傳送的資料。

## 傳回類型

**New-CsMeetingConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.MeetingConfiguration 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsMeetingConfiguration](get-csmeetingconfiguration.md)  
[Remove-CsMeetingConfiguration](remove-csmeetingconfiguration.md)  
[Set-CsMeetingConfiguration](set-csmeetingconfiguration.md)

