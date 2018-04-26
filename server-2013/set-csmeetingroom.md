---
title: Set-CsMeetingRoom
TOCTitle: Set-CsMeetingRoom
ms:assetid: 3dd02280-6407-4e17-929c-7070f8d1c3cf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204831(v=OCS.15)
ms:contentKeyID: 49290685
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsMeetingRoom

 

_**上次修改主題的時間：** 2015-03-09_

修改現有 Lync Server 2013會議室的屬性值。會議室是專為小型會議室之視訊會議及共同作業案例而設計的會議裝置。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsMeetingRoom -Identity <UserIdParameter> [-AcpInfo <MultiValuedProperty>] [-AudioVideoDisabled <$true | $false>] [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-HostedVoiceMail <$true | $false>] [-LineServerURI <String>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-PrivateLine <String>] [-RemoteCallControlTelephonyEnabled <$true | $false>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會更新指派給 RedmondMeetingRoom 會議室的 LineUri。

    Set-CsMeetingRoom -Identity "RedmondMeetingRoom" -LineUri "tel:+12065551219"

## 範例 2

範例 2 會暫時停用 RedmondMeetingRoom 會議室；作法是將 Enabled 屬性設為 False ($False)。

    Set-CsMeetingRoom -Identity "RedmondMeetingRoom" -Enabled $False

若要重新啟用會議室，只要將 Enabled 屬性設為 True ($True) 即可：

    Set-CsMeetingRoom -Identity "RedmondMeetingRoom" -Enabled $True

## 範例 3

範例 3 會暫時停用組織中的所有會議室。為達成此目的，命令會先呼叫不含任何參數 **Get-CsMeetingRoom** Cmdlet，以傳回所有可用會議室的集合。然後，此集合會管線傳送到 **Set-CsMeetingRoom** Cmdlet，以暫時停用集合中的每個會議室。

    Get-CsMeetingRoom | Set-CsMeetingRoom -Enabled $False

## 範例 4

在範例 4 中，組織中的所有會議室都會設定為使用 Lync Server 2013 封存，而不是 Microsoft Exchange Server 封存。為了執行此工作，命令會先使用 **Get-CsMeetingRoom** Cmdlet 傳回所有可用會議室的集合。然後，此集合會管線傳送到 **Set-CsMeetingRoom** Cmdlet，以使用 ExchangeArchivingPolicy Cmdlet 將集合中的每個會議室設定為使用 Lync Server 封存。

    Get-CsMeetingRoom | Set-CsMeetingRoom -ExchangeArchivingPolicy "UseLyncArchivingPolicy"

## 詳細描述

在 Lync Server 中，會議室是安裝在會議室中，提供下列進階會議功能的內建電腦設備：

  - 單鍵加入會議功能

  - 多格檢視視訊庫

  - 在會議室畫面前方提供觸控式白板

  - 整合行事曆供查看排程會議

  - 內容共用及切換

若要管理這些新端點裝置，您必須為裝置建立並啟用 Microsoft Exchange Server 2013資源信箱帳戶，然後再啟用 Lync Server 2013的資源帳戶。請注意，沒有任何 Cmdlet 可以為 Lync Server 建立或移除會議室。您必須使用 [Enable-CsMeetingRoom](enable-csmeetingroom.md) Cmdlet 啟用會議室，以及使用 [Disable-CsMeetingRoom](disable-csmeetingroom.md) Cmdlet 停用會議室。另外還必須有資源帳戶，才可啟用會議室。停用會議室只會從會議室集合中移除該會議室，而不會刪除資源信箱帳戶。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsMeetingRoom"}

Lync Server 控制台：**Set-CsMeetingRoom** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>UserIDParameter</p></td>
<td><p>指出所要修改之會議室的 Identity。會議室 Identity 通常會以下列四種格式之一來指定：1) 會議室的 SIP 位址；2) 會議室的使用者主體名稱 (UPN)；3) 會議室的網域名稱和登入名稱，必須是「網域\登入」格式 (例如，litwareinc\room14)；以及 4) 會議室的 Active Directory 顯示名稱 (例如 Room 14)。您也可以利用會議室的 Active Directory 辨別名稱來參照會議室。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>AcpInfo</em></p></td>
<td><p>選用</p></td>
<td><p>多值屬性</p></td>
<td><p>可讓您將一或多個第三方音訊會議提供者指派給會議室。但是，建議您使用 <strong>Set-UserAcp</strong> Cmdlet 來指派音訊會議提供者。</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioVideoDisabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>表示是否允許會議室使用 Lync 2013 來撥打音訊/虛擬 (A/V) 電話。如果設為 True，會議室將大幅受限於傳送和接收立即訊息。</p>
<p>如果會議室目前已啟用遠端呼叫控制、Enterprise Voice 及/或網際網路通訊協定專用交換機 (IP-PBX) 軟體電話路由，則無法停用 A/V 通訊。</p></td>
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
<td><p>FQDN</p></td>
<td><p>可讓您連線至指定的網域控制站，以擷取會議室資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-dc-001) 或其完整網域名稱 (FQDN) (例如，atl-dc-001.litwareinc.com)。</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>指出會議室是否已啟用 Lync Server 2013。如果您將此值設為 False，會議室就無法再登入 Lync Server；將此值設為 True 可重新啟用會議室的登入權限。</p>
<p>如果使用 Enabled 參數來停用帳戶，則會保留與該帳戶相關聯的資訊 (包括指派的原則以及會議室是否已啟用企業語音及/或遠端呼叫控制)。如果之後使用 Enabled 參數來重新啟用帳戶，將會還原相關聯的帳戶資訊。這不同於使用 <strong>Disable-CsMeetingRoom</strong> Cmdlet 以停用會議室帳戶。當您執行 Disable-CsMeetingRoom 時，將會刪除與該帳戶相關聯的所有 Lync Server 資料。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>指出會議室是否已啟用 Enterprise Voice，這是 Microsoft 的 Voice over Internet Protocol (VoIP) 實作。透過 Enterprise Voice，會議室可以使用網際網路來撥打電話，而非使用標準電話網路。</p></td>
</tr>
<tr class="even">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>指出將如何封存會議室的即時訊息和會議工作階段，以及封存在哪裡。允許的值為：</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* NoArchiving</p>
<p>* ArchivingToExchange</p></td>
</tr>
<tr class="odd">
<td><p><em>HostedVoiceMail</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>此參數設為 True 時，可讓會議室的語音信箱通話路由傳送至託管型版本的 Microsoft Exchange Server 2013。此外，將此選項設為 True 可讓會議室直接撥打到另一位使用者的語音信箱。</p></td>
</tr>
<tr class="even">
<td><p><em>LineServerURI</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>指派給會議室之遠端呼叫控制電話閘道的 URI。LineServerUri 就是閘道 URI，開頭加上 &quot;sip:&quot;。例如：</p>
<p>-LineServerUri &quot;sip:rccgateway@litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>指派給會議室的電話號碼。指定線路統一資源識別元 (URI) 時必須使用 E.164 格式，並使用 &quot;TEL:&quot; 首碼。例如：</p>
<p>-LineUri &quot;TEL:+14255551297&quot;</p>
<p>任何分機號碼都應該新增至線路 URI 的尾端，例如：</p>
<p>-LineUri &quot;TEL:+14255551297;ext=51297&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>可讓您經由管線傳遞代表所要修改之會議室的會議室物件。根據預設， <strong>Set-CsMeetingRoom</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>PrivateLine</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>會議室專用電話線的電話號碼。專用線路是指未發佈在 Active Directory 網域服務 (AD DS) 中的電話號碼，因此其他人無法立即得知。此外，此專用線路會略過大部分的撥入電話路由規則；例如，專用線路來電不會轉接給會議室的代理人。專用線路通常用於個人電話，或應該與其他小組成員分開使用的商務電話。</p>
<p>指定專用線路值時應該採用 E.164 格式，並在開頭加上 &quot;TEL:&quot; 首碼。例如：</p>
<p>-PrivateLine &quot;TEL:+14255551297&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>RemoteCallControlTelephonyEnabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>指出是否已為會議室啟用遠端呼叫控制電話。啟用遠端呼叫控制時，會議室可以利用 Lync Server 2013接聽撥打到其桌面電話的來電。也可以使用 Lync 來撥打電話。這些電話全部依賴標準電話網路，又稱為公用交換電話網路 (PSTN)。若要透過網際網路撥打和接聽電話，必須讓會議室能夠使用 Enterprise Voice。如需詳細資訊，請參閱 EnterpriseVoiceEnabled 參數。</p>
<p>若要使用遠端呼叫控制，會議室也必須具有 LineUri 和 LineServerUri。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>可讓會議室使用 SIP 裝置 (例如 Lync 2013) 來進行通訊的唯一識別碼 (類似電子郵件地址)。SIP 位址必須使用 sip: 首碼，以及有效的 SIP 網域，例如：</p>
<p>-SipAddress &quot;sip:room14@litwareinc.com&quot;</p></td>
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

**Set-CsMeetingRoom** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.ADConnect.Schema.OCSADMeetingRoom 物件執行個體。

## 傳回類型

無。反之， **Set-CsMeetingRoom** Cmdlet 會修改現有的 Microsoft.Rtc.Management.ADConnect.Schema.OCSADMeetingRoom 物件執行個體。

## 請參閱

#### 其他資源

[Disable-CsMeetingRoom](disable-csmeetingroom.md)  
[Enable-CsMeetingRoom](enable-csmeetingroom.md)  
[Get-CsMeetingRoom](get-csmeetingroom.md)  
[Move-CsMeetingRoom](move-csmeetingroom.md)

