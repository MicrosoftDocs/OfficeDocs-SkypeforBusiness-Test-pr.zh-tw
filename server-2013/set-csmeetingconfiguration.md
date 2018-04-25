---
title: Set-CsMeetingConfiguration
TOCTitle: Set-CsMeetingConfiguration
ms:assetid: 80c3529e-d009-48c5-835a-3740f02b6dd4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398648(v=OCS.15)
ms:contentKeyID: 49291485
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsMeetingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

**Set-CsMeetingConfiguration** Cmdlet 可讓您修改組織目前所使用的會議組態設定。會議組態設定可用於指定使用者所能建立的會議 (又稱為電話會議) 類型，以及控制匿名使用者和電話撥入式會議使用者如何 (或能否) 加入這些會議。請注意，這些設定只會影響排程會議，而不會影響在 Lync 中按一下 \[立即開會\] 選項所建立的臨時會議。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsMeetingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsMeetingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AdmitAnonymousUsersByDefault <$true | $false>] [-AssignedConferenceTypeByDefault <$true | $false>] [-Confirm [<SwitchParameter>]] [-CustomFooterText <String>] [-DesignateAsPresenter <None | Company | Everyone>] [-EnableAssignedConferenceType <$true | $false>] [-Force <SwitchParameter>] [-HelpURL <String>] [-LegalURL <String>] [-LogoURL <String>] [-PstnCallersBypassLobby <$true | $false>] [-RequireRoomSystemsAuthorization <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改指派給 Redmond 網站 (-Identity site:Redmond) 的會議組態設定。在此範例中，DesignateAsPresenter 屬性值會設為 Everyone。

    Set-CsMeetingConfiguration -Identity site:Redmond -DesignateAsPresenter Everyone

## 範例 2

範例 2 所示的命令是範例 1 所示命令的變化。但此範例會修改組織所使用之所有會議組態設定的 DesignateAsPresenter 屬性值。為達成此目的，會先呼叫不含任何參數的 **Get-CsMeetingConfiguration** Cmdlet，以傳回目前所使用之所有會議組態設定的集合。然後再將該集合管線傳送至 **Set-CsMeetingConfiguration** Cmdlet，以修改集合中每個項目的 DesignateAsPresenter 屬性。

    Get-CsMeetingConfiguration | Set-CsMeetingConfiguration -DesignateAsPresenter Everyone

## 範例 3

範例 3 會修改所有不允許預設讓匿名使用者參與的會議組態設定。為了執行此工作，命令會先呼叫 **Get-CsMeetingConfiguration** Cmdlet，以傳回目前所使用之所有會議組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 AdmitAnonymousUsersByDefault 屬性等於 False 的設定。接著將篩選後的集合管線傳送至 **Set-CsMeetingConfiguration** Cmdlet，以將該集合中每個項目的 PstnCallersBypassLobby 屬性設為 True。

    Get-CsMeetingConfiguration | Where-Object {$_.AdmitAnonymousUsersByDefault -eq $False} | Set-CsMeetingConfiguration -PstnCallersBypassLobby $True

## 詳細描述

會議是 Lync Server 不可或缺的一部分。CsMeetingConfiguration Cmdlet 可讓系統管理員控制使用者可以建立的會議類型，並決定會議處理匿名使用者與電話撥入式會議使用者的方式。例如，您可以設定會議，以便自動准許透過公用交換電話網路 (PSTN) 撥入的任何人加入會議。或者，您也可以設定會議，不自動允許電話撥入式使用者加入會議，而是送往會議大廳。這些電話撥入式使用者會一直停留在大廳，直到主持人准許他們加入會議為止。

如前所述，這些設定只會影響排程會議，而不會影響在 Microsoft Lync 中按一下 \[立即開會\] 所建立的臨時會議。當您按一下 \[立即開會\] 建立會議時，會自動開啟所有人的參與者存取權，且匿名使用者可以加入會議，而不需要在大廳中等候。不論您如何使用 CsMeetingConfiguration Cmdlet 設定會議設定，都會發生此情況。

**Set-CsMeetingConfiguration** Cmdlet 可讓您修改組織中目前使用的任何會議組態設定集合。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsMeetingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsMeetingConfiguration"}

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
<td><p><em>AdmitAnonymousUsersByDefault</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定會議預設是否允許匿名使用者 (即未驗證的使用者) 參與。如果您想讓新的會議預設允許匿名使用者參與，請將此值設為 True。如果您希望新的會議預設不允許匿名使用者參與，請將此值設為 False。預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>AssignedConferenceTypeByDefault</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定預設是否將新的會議設作公開會議。將此值設為 True，則預設會使用公開會議；將此值設為 False，則預設會使用私人會議。預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>CustomFooterText</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要用在自訂會議邀請函上的文字。</p></td>
</tr>
<tr class="odd">
<td><p><em>DesignateAsPresenter</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.DesignateAsPresenter</p></td>
<td><p>表示當使用者加入會議時，自動指定哪些使用者為主持人 (除了會議召集人)。有效的選項為：None、Company 和 Everyone。根據預設，DesignateAsPresenter 設為 Company，代表組織中的每個人加入會議後，都有主持人的權限。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableAssignedConferenceType</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否允許使用者排定公開會議。在公開會議中，每次舉行會議時，會議識別碼和會議連結會保持一致。在私人會議中，會議識別碼和會議連結會隨著會議而有所不同。預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>HelpURL</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可協助使用者參加會議的網站 URL。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示您要修改之會議組態設定集合的唯一識別碼。若要參考全域設定，請使用下列語法：-Identity global。若要參照在此網站範圍設定的集合，請使用如下語法：-Identity &quot;site:Redmond&quot;。您可以使用如下語法，參考在服務範圍設定的設定：-Identity &quot;service:UserServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>若未指定此參數，則 <strong>Set-CsMeetingConfiguration</strong> Cmdlet 會修改全域設定。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>MeetingConfiguration 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
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
<td><p>表示是否應自動允許以公用交換電話網路 (PSTN) 電話線路撥進的使用者加入會議。如果設為 True ($True)，PSTN 來電者會自動獲准加入會議。如果設為 False ($False)，則 PSTN 來電者會在一開始便被轉到會議大廳。在此情況下，他們必須以通話保留狀態進行等候，直到會議主持人授與其存取會議的權限為止。預設值為 True。</p></td>
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
<td><p>會議組態設定將被修改的 Office 365 租用戶帳戶全域唯一識別碼 (GUID)。</p>
<p>例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>如果您正在使用 Windows PowerShell 的遠端工作階段，並且僅連線至 商務用 Skype Online，您不需要包含 Tenant 參數，而是將會根據您的連線資訊自動填入租用戶 ID。Tenant 參數主要用於混合部署。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.MeetingConfiguration 物件。 Set-CsMeetingConfiguration Cmdlet 接受管線傳送的會議組態物件執行個體。

## 傳回類型

**Set-CsMeetingConfiguration** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.MeetingConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsMeetingConfiguration](get-csmeetingconfiguration.md)  
[New-CsMeetingConfiguration](new-csmeetingconfiguration.md)  
[Remove-CsMeetingConfiguration](remove-csmeetingconfiguration.md)

