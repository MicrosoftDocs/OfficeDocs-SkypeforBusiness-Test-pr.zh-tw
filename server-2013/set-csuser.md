---
title: Set-CsUser
TOCTitle: Set-CsUser
ms:assetid: 6c452df7-75c9-4d94-86bc-4990d718ffe9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398510(v=OCS.15)
ms:contentKeyID: 49291229
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUser

 

_**上次修改主題的時間：** 2015-03-09_

修改現有使用者帳戶的 Lync Server 屬性。只有可以使用 Lync Server 的帳戶，才可修改這些屬性。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsUser -Identity <UserIdParameter> [-AcpInfo <MultiValuedProperty>] [-AudioVideoDisabled <$true | $false>] [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-HostedVoiceMail <$true | $false>] [-LineServerURI <String>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-PrivateLine <String>] [-RemoteCallControlTelephonyEnabled <$true | $false>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，**Set-CsUser** Cmdlet 是用來修改 Identity 為 Pilar Ackerman 的使用者帳戶。此範例會修改帳戶來啟用企業語音 (Microsoft 的 VoIP 實作)。作法是加入 EnterpriseVoiceEnabled 參數，並將參數值設為 $True。

    Set-CsUser -Identity "Pilar Ackerman" -EnterpriseVoiceEnabled $True

## 範例 2

在範例 2 中，財務部門的所有使用者都已啟用帳戶的企業語音。此命令會先使用 **Get-CsUser** Cmdlet 和 LdapFilter 參數，以傳回在財務部門工作之所有使用者的集合。然後再將該資訊管線傳送到 **Set-CsUser** Cmdlet，以啟用集合中每個帳戶的企業語音。

    Get-CsUser -LdapFilter "Department=Finance" | Set-CsUser -EnterpriseVoiceEnabled $True

## 詳細描述

**Set-CsUser** Cmdlet 可讓您修改 Active Directory 網域服務中儲存的 Lync Server 相關使用者帳戶屬性。例如，您可以停用或重新啟用使用者的 Lync Server；啟用或停用使用者的音訊/視訊 (A/V) 通訊；或者修改使用者的專用線路及線路 URI 號碼。**Set-CsUser** Cmdlet 僅適用於已啟用 Lync Server 的使用者。

使用 **Set-CsUser** Cmdlet 修改的屬性只是與 Lync Server 相關的屬性。此 Cmdlet 無法用來修改其他使用者帳戶屬性，例如使用者的工作職稱或部門。但是請記住，Lync Server 屬性應僅使用 Set-CsUser Cmdlet 或 Lync Server \[控制台\] 進行修改。您不應嘗試手動設定這些屬性。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsUser** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUser\\b"}

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
<td><p>UserIdParameter</p></td>
<td><p>表示要修改之使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。也可以透過使用者的 Active Directory 辨別名稱來參考使用者識別。</p>
<p>使用顯示名稱做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回顯示名稱結尾為字串值 &quot; Smith&quot; 的所有使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>AcpInfo</em></p></td>
<td><p>選用</p></td>
<td><p>MultiValuedProperty</p></td>
<td><p>可讓您將一個或多個第三方音訊會議提供者指派給使用者。但是，建議您使用 <strong>Set-UserAcp</strong> Cmdlet 來指派音訊會議提供者。</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioVideoDisabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>表示是否允許使用者使用 Lync 來撥打音訊/虛擬 (A/V) 電話。此參數若設為 True，使用者將大幅受限於傳送和接收立即訊息。</p>
<p>如果使用者目前已啟用遠端呼叫控制、Enterprise Voice 和/或網際網路通訊協定專用交換機 (IP-PBX) 軟體電話路由，則您無法停用 A/V 通訊。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Fqdn</p></td>
<td><p>可讓您指定修改使用者帳戶時要連線的網域控制站。若未加入此參數，則該 Cmdlet 將會使用第一個可用的網域控制站。</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>布林值</p></td>
<td><p>表示使用者是否已啟用 Lync Server。如果您將此值設為 False，使用者就無法再登入 Lync Server；將此值設為 True 可重新啟用使用者的登入權限。</p>
<p>如果使用 Enabled 參數來停用帳戶，則會保留與該帳戶相關聯的資訊 (包括指派的原則以及使用者是否已啟用企業語音及 (或) 遠端呼叫控制)。如果之後使用 Enabled 參數來重新啟用帳戶，將會還原相關聯的帳戶資訊。這不同於使用 <strong>Disable-CsUser</strong> Cmdlet 來停用使用者帳戶。當您執行 <strong>Disable-CsUser</strong> Cmdlet 時，將會刪除與該帳戶相關聯的所有 Lync Server 資料。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>選用</p></td>
<td><p>布林值</p></td>
<td><p>表示使用者是否已啟用 Enterprise Voice，這是 Microsoft 的 Voice over Internet Protocol (VoIP) 實作。透過 Enterprise Voice，使用者可以使用網際網路來撥打電話，而非使用標準電話網路。</p></td>
</tr>
<tr class="even">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>指出使用者的立即訊息工作階段封存位置。允許的值為：</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="odd">
<td><p><em>HostedVoiceMail</em></p></td>
<td><p>選用</p></td>
<td><p>布林值</p></td>
<td><p>此參數設為 True 時，可讓使用者的語音信箱通話路由傳送至託管型版本的 Microsoft Exchange Server。此外，將此選項設為 True 可讓 Lync 使用者直接撥打到另一位使用者的語音信箱。</p></td>
</tr>
<tr class="even">
<td><p><em>LineServerURI</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>指派給使用者的遠端呼叫控制電話閘道的 URI。LineServerUri 就是閘道 URI，開頭加上 &quot;sip:&quot;。例如：sip:rccgateway@litwareinc.com</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>指派給使用者的電話號碼。指定線路統一資源識別元 (URI) 時應該採用 E.164 格式，並使用 &quot;TEL:&quot;首碼。例如：TEL:+14255551297。任何分機號碼都應該新增至線路 URI 的尾端，例如：TEL:+14255551297; ext=51297。</p>
<p>很重要的一點是，Lync Server 會將 TEL:+14255551297 和 TEL:+14255551297;ext=51297 視為兩個不同的號碼。如果您將線路 URI TEL:+14255551297 指派給 Ken Myer，然後又將線路 URI TEL:+14255551297;ext=51297 指派給 Pilar Ackerman，這樣的指派會成功，且指派給 Pilar 的號碼不會標幟為重複號碼。這是因為依據您的設定，這兩個號碼實際上是不同的。例如，在有些組織中撥 1-425-555-1297 會將您的電話轉接到 Exchange 自動語音應答。反之，僅撥分機號碼 (51297) 或使用 Lync 來撥出 1-425-555-1297 和分機號碼 51297，就會將您的電話直接轉接給使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>可讓您透過管線傳遞代表要修改其帳戶之使用者的使用者物件。根據預設，<strong>Set-CsUser</strong> Cmdlet 不會透過管線傳遞物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>PrivateLine</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>使用者專用電話線的電話號碼。專用線路是指未發佈在 Active Directory 網域服務 中的電話號碼，因此其他人無法立即得知。此外，此專用線路會略過大部分的撥入電話路由規則；例如，專用線路來電不會轉接給某人的代理人。專用線路通常用於個人電話，或應該與其他小組成員分開使用的商務電話。</p>
<p>指定專用線路值時應該採用 E.164 格式，並在開頭加上 &quot;TEL:&quot; 首碼。例如：TEL:+14255551297。</p></td>
</tr>
<tr class="even">
<td><p><em>RemoteCallControlTelephonyEnabled</em></p></td>
<td><p>選用</p></td>
<td><p>布林值</p></td>
<td><p>表示是否已為使用者啟用遠端呼叫控制電話。啟用遠端呼叫控制時，使用者可以採用 Lync Server 來接聽撥打到其桌面電話的來電。也可以使用 Lync 來撥打電話。這些電話全部依賴標準電話網路，又稱為公用交換電話網路 (PSTN)。若要透過網際網路撥打和接聽電話，使用者必須可使用 Enterprise Voice。如需詳細資訊，請參閱 EnterpriseVoiceEnabled 參數。</p>
<p>若要使用遠端呼叫控制，使用者必須具有 LineUri 和 LineServerUri。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>可讓使用者使用 SIP 裝置 (例如 Lync) 來進行通訊的唯一識別碼 (類似電子郵件地址)。SIP 位址必須使用 sip: 首碼，以及有效的 SIP 網域，例如：-SipAddress sip:kenmyer@litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Set-CsUser** Cmdlet 接受管線傳送的字串值，該值代表已經針對 Lync Server 啟用的使用者帳戶 Identity。此 Cmdlet 也接受管線傳送的 Active Directory 使用者物件執行個體。

## 傳回類型

**Set-CsUser** Cmdlet 不會傳回任何物件。

## 請參閱

#### 其他資源

[Disable-CsUser](disable-csuser.md)  
[Enable-CsUser](enable-csuser.md)  
[Get-CsUser](get-csuser.md)  
[Move-CsUser](move-csuser.md)

