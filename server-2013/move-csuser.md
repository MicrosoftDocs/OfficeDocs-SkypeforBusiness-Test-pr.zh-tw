---
title: Move-CsUser
TOCTitle: Move-CsUser
ms:assetid: 6fbdbab6-8a8c-421c-b16c-2319be4b8915
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398528(v=OCS.15)
ms:contentKeyID: 49291263
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsUser

 

_**上次修改主題的時間：** 2015-03-09_

將可使用 Lync Server 的一或多個使用者帳戶移至新的登錄器集區。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Move-CsUser -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-HostedMigrationOverrideUrl <String>] [-IgnoreBackendStoreException <SwitchParameter>] [-MoveConferenceData <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會使用 **Move-CsUser** Cmdlet 將 Identity 為 Pilar Ackerman 的使用者帳戶移至 atl-cs-001.litwareinc.com 登錄器集區。

    Move-CsUser -Identity "Pilar Ackerman" -Target "atl-cs-001.litwareinc.com"

## 範例 2

在範例 2 中，Finance 組織單位 (OU) 中的所有使用者帳戶都會移至 atl-cs-001.litwareinc.com 登錄器集區。為了執行此工作，命令會先使用 **Get-CsUser** Cmdlet 並搭配 OU 參數，以擷取 Finance OU 中所有使用者帳戶的集合。擷取資料之後，會將資訊管線傳送到 **Move-CsUser** Cmdlet，以將集合中的每個帳戶移至 atl-cs-001.litwareinc.com 登錄器集區。

    Get-CsUser -OU "ou=Finance,dc=litwareinc,dc=com" | Move-CsUser -Target "atl-cs-001.litwareinc.com"

## 範例 3

範例 3 使用 **Move-CsUser** Cmdlet 將 Identity 為 Pilar Ackerman 的使用者帳戶移至 atl-cs-001.litwareinc.com 登錄器集區。此外，使用 Force 參數來確保只移動帳戶本身，與該帳戶相關聯的資料 (例如 Pilar 已排程的會議) 不會移動，而是捨棄。只有當您嘗試不使用 Force 參數呼叫 **Move-CsUser** Cmdlet，但移動失敗時，才需要使用 Force 參數。

    Move-CsUser -Identity "Pilar Ackerman" -Target "atl-cs-001.litwareinc.com" -Force

## 詳細描述

**Move-CsUser** Cmdlet 可讓您將啟用 Lync Server 的使用者帳戶從一個登錄器集區移至另一個。**Move-CsUser** Cmdlet 只會影響使用者的 Lync Server 帳戶位置；不會將使用者的 Active Directory 帳戶移至新的組織單位 (OU) 或其他新位置。

如果 Lync Server 與 Office Communications Server 2007 R2 或 Office Communications Server 2007 並存，則可使用 **Move-CsUser** Cmdlet 將使用者從 Lync Server 移回 Office Communications Server 的舊版安裝。若要將使用者移回 Office Communications Server，請對 Target 參數指派舊版集區的完整網域名稱 (FQDN)。如果這樣做，請記住移回 Office Communications Server 的使用者可能會發生功能與資料遺失；這是因為 Lync Server 的功能比 Office Communications Server 2007 或 Office Communications Server 2007 R2 功能更多。移回的使用者可能需要安裝舊版的用戶端軟體，也可能需要重新排定當他們的使用者帳戶屬於 Lync Server 時所建立的會議。

若要將使用者從 Communications Server 2007 或 Communications Server 2007 R2 移到 Lync Server，請使用 **Move-CsLegacyUser** Cmdlet。**Move-CsUser** Cmdlet 是設計來將使用者從一個 Lync Server 移到另一個 Lync Server 集區，或將使用者從 Lync Server 集區移到 Office Communications Server 集區。Move-CsLegacyUser 可將使用者從 Office Communications Server 移到 Lync Server。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Move-CsUser** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsUser"}

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
<td><p>表示要移動之使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。也可以透過使用者的 Active Directory 辨別名稱來參考使用者識別。</p>
<p>使用「顯示名稱」做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會傳回所有顯示名稱結尾為字串值 &quot; Smith&quot; 的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>應移動其使用者帳戶之登錄器集區的 FQDN (例如，atl-cs-001.litwareinc.com)。除了登錄器集區外，Target 也可以是舊版 Office Communications Server 前端伺服器或主機供應商的 FQDN。移到主機供應商 (例如 Microsoft Lync Online 2010) 的所有帳戶將會遺失所有相關聯的使用者資料。例如，會刪除使用者已排定的所有會議，而且在 Lync Online 2010 中無法使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您略過確認提示，否則當您嘗試移動使用者時，會出現該確認提示。若要略過確認提示，請使用下列語法並包含 Confirm 參數：</p>
<p>-Confirm:$False</p>
<p>如果希望出現確認提示，請使用下列語法：</p>
<p>-Confirm</p></td>
</tr>
<tr class="even">
<td><p><em>Credential</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>可讓您以替代認證來執行 Move-CsUser Cmdlet。如果您用來登入 Windows 的帳戶不具有使用者物件所需的必要權限，可能就需要此參數。</p>
<p>若要使用 Credential 參數，您必須先使用 <strong>Get-Credential</strong> Cmdlet 來建立 PSCredential 物件。如需詳細資訊，請參閱 <strong>Get-Credential</strong> Cmdlet 說明主題。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以擷取連絡人資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-cs-001) 或其 FQDN (例如，atl-cs-001.litwareinc.com)。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，會移動使用者帳戶，但刪除任何關聯的資料 (例如使用者已排定的會議)。若未設定，則會移動帳戶與關聯的資料。</p></td>
</tr>
<tr class="odd">
<td><p><em>HostedMigrationOverrideUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>將使用者移至 商務用 Skype Online 時所使用之代管移轉服務的 URL。</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會指示電腦忽略後端資料庫可能發生的任何錯誤，並嘗試移動使用者，而不管那些錯誤。</p></td>
</tr>
<tr class="odd">
<td><p><em>MoveConferenceData</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會將所傳送之使用者的會議資料移至不同的登錄器集區。請注意，如果您是在災害復原程序中移動使用者，請勿使用 MoveConferenceData 參數。在災害復原程序中，您應該要利用備份服務來移動會議資料。</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您透過管線傳遞代表要移動之使用者帳戶的使用者物件。根據預設，<strong>Move-CsUser</strong> Cmdlet 不會透過管線傳遞物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>ProxyPool</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>此參數只能用於 Lync Online。請勿用於 Lync Server 的內部部署實作。</p></td>
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

字串或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Move-CsUser** Cmdlet 接受管線傳送的字串值，該值代表已經針對 Lync Server 啟用的使用者帳戶 Identity。此 Cmdlet 也接受管線傳送的 Active Directory 使用者物件執行個體。

## 傳回類型

**Move-CsUser** Cmdlet 不會傳回值或物件，而會修改 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsUser](get-csuser.md)  
[Move-CsLegacyUser](move-cslegacyuser.md)

