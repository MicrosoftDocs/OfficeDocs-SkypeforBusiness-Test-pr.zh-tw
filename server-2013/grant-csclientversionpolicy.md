---
title: Grant-CsClientVersionPolicy
TOCTitle: Grant-CsClientVersionPolicy
ms:assetid: b94d9473-db5f-4350-a7b4-991d0e26e525
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412903(v=OCS.15)
ms:contentKeyID: 49292111
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsClientVersionPolicy

 

_**上次修改主題的時間：** 2015-03-09_

在全域、網站、服務或個別使用者範圍指派用戶端版本原則。用戶端版本原則可讓您指定可以登入您 Lync Server 系統的用戶端 (如 Microsoft Office Communicator 2007 R2)。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Grant-CsClientVersionPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，用戶端版本原則 RedmondClientVersionPolicy 指派給使用者 Ken Myer。

    Grant-CsClientVersionPolicy -Identity "Ken Myer" -PolicyName "RedmondClientVersionPolicy"

## 範例 2

範例 2 所示的命令會將用戶端版本原則 RedmondClientVersionPolicy 指派給所有在 Redmond 城市工作的使用者。為達成此目的，命令會先使用 **Get-CsUser** Cmdlet 搭配 LdapFilter 參數，以擷取適當的使用者帳戶集合；篩選值 "l=Redmond" (其中 "l" 是小寫字母的 L，適用於 "locality" 的 LDAP 屬性名稱) 可將擷取資料的範圍限制在 Redmond 城市工作的使用者。接著將此集合傳送到 **Grant-CsClientVersionPolicy** Cmdlet，以將指定的原則指派給集合中的每位使用者。

    Get-CsUser -LdapFilter "l=Redmond" | Grant-CsClientVersionPolicy -PolicyName "RedmondClientVersionPolicy"

## 範例 3

範例 3 會將用戶端版本原則 RedmondClientVersionPolicy 指派給指定組織單位 OU 中的所有使用者。為了完成此工作，命令先呼叫 **Get-CsUser** Cmdlet 搭配 OU 參數；此參數值表示 OU 的辨別名稱，系統會將用戶端版本原則指派給此 OU 的使用者 (ou=Redmond,ou=North America,dc=litwareinc,dc=com)。擷取使用者帳戶後，會將集合管線傳送到 **Grant-CsClientVersionPolicy** Cmdlet，以將 RedmondClientVersionPolicy 指派給這其中每一位使用者。

    Get-CsUser -OU "ou=Redmond,ou=North America,dc=litwareinc,dc=com" | Grant-CsClientVersionPolicy -PolicyName "RedmondClientVersionPolicy"

## 範例 4

範例 4 會將用戶端版本原則 RedmondClientVersionPolicy 指派給所有先前已指派語音原則 RedmondVoicePolicy 的使用者。為達成此目的，命令會先呼叫 **Get-CsUser** Cmdlet 搭配 Filter 參數；篩選值 {VoicePolicy -eq "RedmondVoicePolicy"} 可確保只會傳回 VoicePolicy 屬性等於 "RedmondVoicePolicy" 的使用者帳戶。然後將產生的使用者帳戶管線傳送到 **Grant-CsClientVersionPolicy** Cmdlet，以指派用戶端版本原則 RedmondClientVersionPolicy。

    Get-CsUser -Filter {VoicePolicy -eq "RedmondVoicePolicy"} | Grant-CsClientVersionPolicy -PolicyName "RedmondClientVersionPolicy"

## 範例 5

範例 5 會為組織內的所有使用者取消指派先前指派給他們的所有個別使用者用戶端版本原則。為達成此目的，命令會先使用 **Get-CsUser** Cmdlet，以傳回組織中已針對 Lync Server 啟用的所有使用者集合。然後，此集合會管線傳送到 **Remove-CsClientVersionPolicy** Cmdlet，以移除所有已指派給那些使用者的個別使用者用戶端版本原則。作法是將 PolicyName 參數值設為 $null。

    Get-CsUser | Grant-CsClientVersionPolicy -PolicyName $Null

## 詳細描述

用戶端版本原則代表用戶端版本規則的集合；而用戶端版本規則用於決定允許登入 Lync Server 的用戶端應用程式。當使用者嘗試登入 Lync Server 時，該使用者的用戶端應用程式會傳送 SIP 標頭給伺服器，這個標頭包含與應用程式本身有關的詳細資訊，包括軟體的主要版本、次要版本及組建編號。然後系統會根據用戶端版本規則的集合，檢查 SIP 標頭所含的版本資訊，查看是否有任何規則要套用至該特定應用程式。如果有這樣的規則， Lync Server 就會採取此規則指定的行動。例如，規則可能會告知 Lync Server 允許登入、封鎖登入，或允許登入，但是會以無訊息方式將用戶端應用程式更新為最新版本 (例如，將 Office Communicator 2007 R2 更新到 Lync 2013)。

用戶端版本原則 (可套用至全域範圍、網站範圍、服務範圍 (僅登錄器服務)，或個別使用者範圍)，可讓您在決定哪些用戶端應用程式可用來存取系統時，擁有彈性。例如，您可能想防止使用者使用 Communicator 2007 R2 登入 Lync Server，畢竟這個舊版的用戶端應用程式與 Lync 所支援的功能和特性並不同。但是，由於硬體或軟體衝突，您可能也想選取一群不能升級為 Lync 的使用者。在該情況下，您可以建立個別的規則 (以及個別的用戶端版本原則)，允許那些使用者從 Communicator 2007 R2 登入。

**Grant-CsClientVersionPolicy** Cmdlet 讓您可以將用戶端版本原則指派給個別使用者。當您建立個別使用者原則時，該原則不會自動指派給任何人；除非您呼叫 **Grant-CsClientVersionPolicy** Cmdlet 將原則明確指派給一位或一組使用者，否則指派不會生效。

請注意，用戶端版本原則不適用於同盟使用者；而是同盟使用者受到本身組織中使用的用戶端版本原則所約束。例如，假設某位同盟使用者使用用戶端 A (此為同盟組織所允許的用戶端)。只要同盟組織允許使用用戶端 A，這個使用者就可以使用該用戶端與您的組織通訊。即使您的用戶端版本原則會封鎖使用用戶端 A，此情況也成立。在您組織中強制執行的用戶端版本原則不會覆寫同盟組織中使用者的用戶端版本原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Grant-CsClientVersionPolicy** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsClientVersionPolicy"}

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
<td><p>指出要將原則指派給哪一個使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。也可以透過使用者的 Active Directory 辨別名稱來參考使用者識別。</p>
<p>此外，使用顯示名稱做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會傳回所有顯示名稱結尾為字串值 &quot; Smith&quot; 的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>要指派之原則的「名稱」。簡單來說，PolicyName 是原則 Identity 減去原則範圍 (&quot;tag:&quot;)。例如，對於 Identity 為 tag:Redmond 的原則，其 PolicyName 等於 Redmond；對於 Identity 為 tag:RedmondClientVersionPolicy 原則，其 PolicyName 等於 RedmondClientVersionPolicy。若要取消指派先前已指派給使用者的個別使用者原則，請將 PolicyName 設定為 Null 值 ($null)。</p></td>
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
<td><p>可讓您指定指派原則時連線的網域控制站。若未加入此參數，Cmdlet 會使用第一個可用的網域控制站。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，會使得 Cmdlet 透過 Windows PowerShell 管線傳遞一或多個使用者物件。根據預設， <strong>Grant-CsClientVersionPolicy</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
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

字串值或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。 **Grant-CsClientVersionPolicy** Cmdlet 會接受代表使用者帳戶 Identity 之字串值的管線傳送資料。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

根據預設， **Grant-CsClientVersionPolicy** Cmdlet 不會傳回物件或值。但是，如果加入 PassThru 參數，則 Cmdlet 會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsClientVersionPolicy](get-csclientversionpolicy.md)  
[New-CsClientVersionPolicy](new-csclientversionpolicy.md)  
[Remove-CsClientVersionPolicy](remove-csclientversionpolicy.md)  
[Set-CsClientVersionPolicy](set-csclientversionpolicy.md)

