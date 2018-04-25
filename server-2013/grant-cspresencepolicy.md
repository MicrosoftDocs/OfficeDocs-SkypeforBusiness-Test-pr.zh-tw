---
title: Grant-CsPresencePolicy
TOCTitle: Grant-CsPresencePolicy
ms:assetid: 756c08a7-26b0-4ea8-816b-b33ebcac51aa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398571(v=OCS.15)
ms:contentKeyID: 49291338
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsPresencePolicy

 

_**上次修改主題的時間：** 2015-03-09_

將個別使用者的目前狀態原則授與使用者或使用者群組。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Grant-CsPresencePolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將個別使用者顯示狀態原則 RedmondPresencePolicy 指派給單一使用者：含有 Identity Ken Myer 的使用者。

    Grant-CsPresencePolicy -Identity "Ken Myer" -PolicyName "RedmondPresencePolicy"

## 範例 2

範例 2 會將目前狀態原則 RedmondPresencePolicy 指派給在 Active Directory 網域服務之 Redmond OU 中擁有帳戶的所有使用者。為達成此目的，命令會先使用 **Get-CsUser** Cmdlet 並搭配 OU 參數，以傳回所有在 Redmond OU (OU=Redmond,dc=litwareinc,dc=com) 中找到之使用者帳戶的集合。然後，此集合會管線傳送到 **Grant-CsPresencePolicy** Cmdlet，以將 RedmondPresencePolicy 原則指派給集合中的每位使用者。

    Get-CsUser -OU "OU=Redmond,dc=litwareinc,dc=com" | Grant-CsPresencePolicy -PolicyName "RedmondPresencePolicy"

## 範例 3

範例 3 會將 RedmondPresencePolicy 原則指派給在 Redmond 市工作的所有使用者。為了執行此工作，命令會先使用 **Get-CsUser** Cmdlet 並搭配 LdapFilter 參數，以傳回在 Redmond 工作之所有使用者的集合；篩選值 "l=Redmond" 可將傳回的資料限制在 Redmond 的使用者 (在 LDAP 的查詢語言中，l (L 的小寫) 是「位置」的簡稱。接著將擷取的集合管線傳送到 **Grant-CsPresencePolicy** Cmdlet，以將 RedmondPresencePolicy 指派給集合中的每位使用者。

    Get-CsUser -LdapFilter "l=Redmond" | Grant-CsPresencePolicy -PolicyName "RedmondPresencePolicy"

## 範例 4

範例 4 所示的命令會解除指派所有原先指派給在 Redmond 工作之使用者的個別使用者目前狀態原則。透過呼叫 **Grant-CsPresencePolicy** Cmdlet 並將 PolicyName 參數設為 Null 值 ($Null)，會使 Cmdlet 移除任何受命令影響之已指派給使用者的個別使用者目前狀態原則。

    Get-CsUser -LdapFilter "l=Redmond" | Grant-CsPresencePolicy -PolicyName $Null

## 詳細描述

目前狀態資訊十分有價值，它可讓您知道連絡人是否可參與立即訊息交談。但同時，使用目前狀態資訊也是有代價的：目前狀態訂閱的愈多，則必須有更多專供更新目前狀態資訊使用的網路頻寬。如果您擔心網路頻寬的問題，可以限制每個人的目前狀態訂閱數。

CsPresencePolicy Cmdlet 可讓您管理目前狀態訂閱的兩個重要層面：已提示訂閱者與類別目錄訂閱。在將您新增到另一個人的 Lync 連絡人清單後，為您設定的預設行為是會收到快顯通知來告知已將您新增到該清單中。一直到您將顯示的對話方塊關閉後，每個通知才能算作已提示訂閱者。目前狀態原則的 MaxPromptedSubscriber 屬性可讓您指定使用者可擁有的未解決通知對話方塊數目上限 (如果使用者到達上限，就不會再收到新的連絡人通知 - 至少在某些對話方塊已解決前不會)。

類別目錄訂閱代表要求特定的資訊目錄，例如要求行事曆資訊的應用程式。MaxCategorySubscription 屬性可讓您設定使用者可擁有的類別目錄訂閱數限制。

Lync Server 之前版本的已提示訂閱者與類別目錄訂閱是全域管理的。透過 **CsPresencePolicy** Cmdlet，您現在可以在全域範圍、網站範圍，甚至是個別使用者範圍管理目前狀態訂閱。這可讓您控制頻寬的使用，同時確保使用者能夠存取工作所需的目前狀態資訊。

建立個別使用者原則時，該原則並沒有自動指派給每個人。而是必須執行 **Grant-CsPresencePolicy** Cmdlet，明確將個別使用者顯示狀態原則指派給使用者 (或使用者群組)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Grant-CsPresencePolicy** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsPresencePolicy"}

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
<td><p>表示要指派顯示狀態原則之使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。也可以使用使用者的 Active Directory 辨別名稱來指定使用者識別。</p>
<p>此外，使用顯示名稱做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回所有顯示名稱是以字串 &quot; Smith&quot; 結束的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指派之個別使用者原則的 Identity；例如：-PolicyName &quot;RedmondPresencePolicy&quot;。PolicyName 是原則 Identity 減去 &quot;tag&quot;：首碼。例如，Identity 為 &quot;tag:NorthAmericaPresencePolicy&quot; 的原則，其 PolicyName 相當於 &quot;NorthAmericaPresencePolicy&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>當指派原則時所要連絡之網域控制站的完整網域名稱 (FQDN)。例如：-DomainController atl-dc-001.litwareinc.com。</p>
<p>若未指定，則當指派原則時 <strong>Grant-CsPresencePolicy</strong> Cmdlet 會與最近的可用網域控制站連絡。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您透過代表已指派原則的使用者之管線傳遞使用者物件。根據預設，<strong>Grant-CsPresencePolicy</strong> Cmdlet 不會透過管線傳遞物件。</p></td>
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

字串值或 Microsoft.Rtc.Management.WritebleConfig.Policy.Presence.PresencePolicy 物件。**Grant-CsPresencePolicy** Cmdlet 接受代表使用者帳戶識別之字串值的管線傳送輸入。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

根據預設，**Grant-CsPresencePolicy** Cmdlet 不會傳回物件或值。但是，如果加入 PassThru 參數，Cmdlet 就會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact 的執行個體。

## 請參閱

#### 其他資源

[Get-CsPresencePolicy](get-cspresencepolicy.md)  
[New-CsPresencePolicy](new-cspresencepolicy.md)  
[Remove-CsPresencePolicy](remove-cspresencepolicy.md)  
[Set-CsPresencePolicy](set-cspresencepolicy.md)

