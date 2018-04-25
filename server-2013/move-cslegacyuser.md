---
title: Move-CsLegacyUser
TOCTitle: Move-CsLegacyUser
ms:assetid: f4b36fc8-17a7-490d-a147-6d77abab0f92
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413025(v=OCS.15)
ms:contentKeyID: 49292819
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsLegacyUser

 

_**上次修改主題的時間：** 2015-03-09_

將一或多個使用者帳戶從 Microsoft Office Communications Server 2007 R2 移轉至 Lync Server 2013。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Move-CsLegacyUser -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-ExcludeArchivingPolicy <SwitchParameter>] [-ExcludeConferencingPolicy <SwitchParameter>] [-ExcludeDialPlan <SwitchParameter>] [-ExcludeExternalAccessPolicy <SwitchParameter>] [-ExcludePresencePolicy <SwitchParameter>] [-ExcludeVoicePolicy <SwitchParameter>] [-Force <SwitchParameter>] [-HostedMigrationOverrideUrl <String>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，使用 **Move-CsLegacyUser** Cmdlet 將使用者帳戶 (Identity 為 Pilar Ackerman) 移轉至登錄器集區 atl-cs-001.litwareinc。因為沒有使用額外的參數，任何原先指派給此帳戶的原則或設定也會跟著移轉。這意味著，如果原先有指派原則 (如撥號對應表) 給 Pilar Ackerman，則移動她的帳戶時，將會指派 Lync Server 2013 等同項目給她。

    Move-CsLegacyUser -Identity "Pilar Ackerman" -Target "atl-cs-001.litwareinc.com"

## 範例 2

範例 2 所示的命令會移轉 Pilar Ackerman 的使用者帳戶，但不會移轉任何原先指派至她帳戶的撥號對應表。當帳戶移轉後，將不會指派撥號對應表給 Pilar。

    Move-CsLegacyUser -Identity "Pilar Ackerman" -Target "atl-cs-001.litwareinc.com" -ExcludeDialPlan 

## 範例 3

在範例 3 中，Finance OU 中的所有使用者帳戶會移至登錄器集區 atl-cs-001.litwareinc.com。為達成此目的，命令會先使用 **Get-CsUser** Cmdlet 和 OU 參數，以擷取 Finance OU 中所有使用者帳戶的集合。然後再於擷取帳戶之後，將該集合以管線傳送到 **Move-CsLegacyUser** Cmdlet，以將每個帳戶移往新登錄器集區。此命令假設 Finance OU 中的所有使用者皆為舊版使用者。

    Get-CsUser -OU "ou=Finance,dc=litwareinc,dc=com" | Move-CsLegacyUser -Target "atl-cs-001.litwareinc.com"

## 範例 4

在範例 4 中，系統使用 Move-CsLegacyUser 將已啟用 Lync Server 但目前尚未指派給登錄器集區的使用者，指派給登錄器集區。在此命令中，會先呼叫 **Get-CsUser** Cmdlet 搭配 UnassignedUser 參數，以傳回目前未指派至登錄器集區的所有使用者集合。此集合接著會傳送到 **Move-CsLegacyUser** Cmdlet，以便將每位使用者指派至集區 atl-cs-001.litwareinc.com。此範例假設所有未指派的使用者均為原有使用者。

    Get-CsUser -UnassignedUser | Move-CsLegacyUser -Target "atl-cs-001.litwareinc.com"

## 詳細描述

許多安裝 Lync Server 2013 的組織也會執行舊版軟體。幸運地是，這不會造成問題，您可以同時執行最新版的軟體及舊版軟體。隨著時間推移，接著您可以開始移轉組態設定及原則，最後則是將使用者帳戶移轉至 Lync Server 2013。

**Move-CsLegacyUser** Cmdlet 不僅讓您可以將使用者移轉至 Lync Server 2013，針對移轉程序也給您相當大的控制權。例如，以最簡單的形式使用時，可以給 **Move-CsLegacyUser** Cmdlet 要移轉之使用者的識別身分以及使用者即將隸屬之 Lync Server 登錄器集區的完整網域名稱 (FQDN)；反過來說，**Move-CsLegacyUser** Cmdlet 會移動使用者帳戶，而且會維護所有原先套用至該帳戶的原則和設定。例如，假設原先在 Communications Server 2007 R2 中有指派撥號對應表給 Ken Myer。根據預設，當您移轉 Ken 的帳戶，撥號對應表也會跟著移轉：這代表 **Move-CsLegacyUser** Cmdlet 會自動把之前指派給 Ken Myer 的撥號對應表的 Lync Server 2013 等同項目指派給他。

當然，這只在您有移轉撥號對應表，且在先前已指派給 Ken Myer 的撥號對應表有 Lync Server 2013 等同項目時才會發生。或者，您可能決定不移轉撥號對應表。在這個情況下，您可以呼叫 **Move-CsLegacyUser** Cmdlet 搭配 ExcludeDialPlan 參數。使用此參數時，撥號對應表就不會跟著使用者帳戶一起移轉：也就是說，系統會移轉 Ken Myer 的使用者帳戶，但不會指派撥號對應表給他 (即使您確實移轉撥號對應表，也會是這個結果；ExcludeDialPlan 參數會阻止系統將撥號對應表指派給已移轉的使用者帳戶)。其他參數可在移轉使用者帳戶時排除語音原則、會議原則、封存原則、外部存取原則，及/或目前狀態原則。

您必須先安裝 Windows Management Instrumentation (WMI) 回溯相容性介面套件，才可以執行 **Merge-CsLegacyTopology** Cmdlet；您可以執行 OCSWMIBC.msi 來安裝此應用程式 (OCSWMIBC.msi 位於安裝 DVD 的 Setup 資料夾中)。安裝相容性介面套件之後，接著就能呼叫 **Merge-CsLegacyUser** Cmdlet，藉此轉移一或多個使用者帳戶。

誰可以執行這個 Cmdlet ？根據預設，下列群組成員已獲得授權，可在本機執行 **Move-CsLegacyUser** Cmdlet：RTCUniversalUserAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsLegacyUser"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>指出要移轉之使用者帳戶的識別身分。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\kenmyer)；以及 4) 使用者的 Active Directory 網域服務顯示名稱 (例如 Ken Myer)。您也可以使用使用者的 Active Directory 辨別名稱來參考使用者識別。</p>
<p>使用「顯示名稱」做為使用者識別時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回所有顯示名稱是以字串 &quot; Smith&quot; 結束的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>使用者帳戶應屬之登錄器集區的 FQDN。例如：-Target atl-cs-001.litwareinc.com。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Credential</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>可讓您以替代認證來執行 Move-CsLegacyUser Cmdlet。如果您用來登入 Windows 的帳戶不具有使用使用者物件所需的必要權限，可能就需要這一項。</p>
<p>若要使用 Credential 參數，必須先使用 Get-Credential Cmdlet 建立 PSCredential 物件。如需詳細資訊，請參閱說明主題＜Get-Credential Cmdlet＞。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>讓您連線至指定的網域控制站，以移動使用者帳戶。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-cs-001) 或其 FQDN (例如，atl-cs-001.litwareinc.com)。</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeArchivingPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>若有使用此參數，在移轉帳戶時不會保留任何指派給使用者帳戶的封存原則。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludeConferencingPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>若有使用此參數，在移轉帳戶時不會保留任何指派給使用者帳戶的會議原則。</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeDialPlan</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>若有使用此參數，在移轉帳戶時不會保留任何指派給使用者帳戶的撥號對應表。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludeExternalAccessPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>若有使用此參數，在移轉帳戶時不會保留任何指派給使用者帳戶的外部存取原則。</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludePresencePolicy</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>若有使用此參數，在移轉帳戶時不會保留任何指派給使用者帳戶的目前狀態原則。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludeVoicePolicy</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>若有使用此參數，在移轉帳戶時不會保留任何指派給使用者帳戶的語音原則。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>HostedMigrationOverrideUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>將使用者移至 Office 365 版之 Lync Server 2013 時所使用之代管移轉服務的 URL。</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會指示電腦忽略後端資料庫可能發生的任何錯誤，並嘗試移動使用者而不管這些錯誤。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>讓您透過管線傳遞使用者物件，代表被移動的使用者帳戶。根據預設，<strong>Move-CsLegacyUser</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>此參數僅能與 Communications Server 2007 R2 搭配使用。請勿用於 Lync Server 的內部部署實作。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Move-CsLegacyUser** Cmdlet 不接受以管線傳送的輸入。

## 傳回類型

**Move-CsLegacyUser** Cmdlet 不會傳回任何值或物件，而會移動 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件的執行個體。

## 請參閱

#### 其他資源

[Import-CsLegacyConfiguration](import-cslegacyconfiguration.md)  
[Import-CsLegacyConferenceDirectory](import-cslegacyconferencedirectory.md)  
[Merge-CsLegacyTopology](merge-cslegacytopology.md)  
[Move-CsUser](move-csuser.md)  
[Set-CsUser](set-csuser.md)

