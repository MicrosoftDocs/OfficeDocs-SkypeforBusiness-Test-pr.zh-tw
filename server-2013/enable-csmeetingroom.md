---
title: Enable-CsMeetingRoom
TOCTitle: Enable-CsMeetingRoom
ms:assetid: 88af3267-80c5-46c0-aaef-135843b42a04
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205062(v=OCS.15)
ms:contentKeyID: 49291572
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsMeetingRoom

 

_**上次修改主題的時間：** 2015-03-09_

啟用 Lync Server 2013 會議室。會議室是專為小型會議室之視訊會議及共同作業案例而設計的會議裝置。若要啟用會議室，必須先建立代表該系統的 Active Directory 使用者帳戶。請注意，雖然會議室物件是以使用者帳戶為基礎，但是當您執行 **Get-CsUser** Cmdlet 時，不會顯示這些物件。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Enable-CsMeetingRoom -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-HostingProviderProxyFqdn <Fqdn>] [-OriginatorSid <SecurityIdentifier>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-RegistrarPool <Fqdn>] [-SipAddress <String>] [-SipAddressType <FirstLastName | EmailAddress | UserPrincipalName | SAMAccountName | None>] [-SipDomain <Fqdn>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會啟用 Identity (在此範例中為 Active Directory 顯示名稱) 為 Redmond Meeting room 的會議室。新會議室會安置在 arl-cs-001.litwareinc.com 登錄器集區上，給定的 SIP 位址為 sip:RedmondMeetingRoom@litwareinc.com。

    Enable-CsMeetingRoom -Identity "Redmond Meeting room" -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddress "sip:RedmondMeetingRoom@litwareinc.com"

## 範例 2

範例 2 會啟用在 MeetingsRoom OU 中找到的所有會議室 (換言之，此命令會啟用 MeetingsRoom OU 中的所有使用者帳戶)。為達成此目的，命令會先呼叫 **Get-CsAdUser** Cmdlet 並搭配 OU 參數；參數值 "OU=MeetingRooms,dc=litwareinc,dc=com" 可將傳回的資料限制在 MeetingsRoom OU 中所找到的使用者帳戶。然後再將這些帳戶管線傳送到 **Enable-CsMeetingRoom** Cmdlet，以將集合中的每個帳戶啟用為會議室。每個新會議室都會安置在 atl-cs-001.litwareinc.com 登錄器集區，並具備由帳戶之 SamAccountName 參數 (例如 room14) 及 litwareinc.com SIP 網域組成的 SIP 位址。

    Get-CsAdUser -OU "OU=MeetingRooms,dc=litwareinc,dc=com" | Enable-CsMeetingRoom -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddressType "SamAccountName" -SipDomain "litwareinc.com"

## 詳細描述

在 Lync Server 中，會議室是安裝在會議室中，提供下列進階會議功能的內建電腦設備：

  - 單鍵加入會議功能

  - 多格檢視視訊庫

  - 在會議室畫面前方提供觸控式白板

  - 整合行事曆供查看排程會議

  - 內容共用及切換

若要管理這些新端點裝置，您必須為裝置建立並啟用 Microsoft Exchange Server 2013 資源信箱帳戶，然後再啟用 Lync Server 2013 的資源帳戶。請注意，沒有任何 Cmdlet 可以為 Lync Server 建立或移除會議室。您必須使用 **Enable-CsMeetingRoom** Cmdlet 啟用會議室，以及使用 [Disable-CsMeetingRoom](disable-csmeetingroom.md) Cmdlet 停用會議室。另外還必須有資源帳戶，才可啟用會議室。停用會議室只會從會議室集合中移除該會議室，而不會刪除資源信箱帳戶。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Enable-CsMeetingRoom"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Enable-CsMeetingRoom** Cmdlet 所執行的功能。

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
<td><p>指出要設成會議室之使用者帳戶的 Identity。識別通常可以使用下列四種格式的其中一種來指定：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\room14)；4) 使用者的 Active Directory 顯示名稱 (例如 Room 14)。</p>
<p>您也可以利用使用者的 Active Directory 辨別名稱來參照使用者帳戶。</p>
<p>使用「顯示名稱」做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會傳回所有顯示名稱結尾為 &quot; Smith&quot; 字串值的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以停用會議室。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如 atl-dc-001) 或其完整網域名稱 (FQDN) (例如 atl-dc-001.litwareinc.com)。</p></td>
</tr>
<tr class="even">
<td><p><em>HostingProviderProxyFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>代管提供者 Proxy 伺服器的完整網域名稱。此參數只能與 Microsoft Lync Online 搭配使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>OriginatorSid</em></p></td>
<td><p>選用</p></td>
<td><p>System.Security.Principal.SecurityIdentifier</p></td>
<td><p>msRTCSIP-OriginatorSID 屬性的值。這個 Active Directory 屬性可用來啟用單一登入。此參數只能與 Microsoft Lync Online 搭配使用。</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您經由管線傳遞代表針對 Lync Server 所要啟用之會議室的會議室物件。根據預設，<strong>Enable-CsMeetingRoom</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>ProxyPool</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Proxy 集區名稱。此參數只能與 Microsoft Lync Online 搭配使用。</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPool</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>指出要用來安置會議室之 Lync Server 帳戶的登錄器集區。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指派特定的 SIP 位址給會議室。指定 SIP 位址時，請在位址開頭加上 &quot;sip:&quot;。這表示提供給 SipAddress 參數的值應該看起來如下：</p>
<p>sip:room14@litwareinc.com</p>
<p>若您使用 SipAddressType 參數以便讓 Lync Server 自動為會議室產生 SIP 位址，則不應使用 SipAddress 參數。</p>
<p>若您嘗試同時啟用多個會議室，則無法使用 SipAddress 參數。您必須改為使用 SipAddressType 參數，為這些會議室自動產生 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddressType</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.Cmdlets.AddressType</p></td>
<td><p>指示 Lync Server 為新會議室自動產生 SIP 位址。為了讓 Lync Server 自動產生 SIP 位址，您必須加上 SipAddressType 參數，並使用下列其中一個參數值：</p>
<p>* FirstLastName。SIP 位址是使用者的名字加句點，再加上使用者的姓氏和 SIP 網域。例如，Room 14 使用者的 SIP 位址類似如下：Room.14@litwareinc.com。若您使用這種位址類型，還必須加入 SipDomain 參數。</p>
<p>* EmailAddress。使用者的電子郵件地址 (如 Active Directory 中定義) 會當做 SIP 位址使用。UserPrincipalName。使用者的 UPN 會當做 SIP 位址使用。</p>
<p></p>
<p>* SamAccountName。SIP 位址是使用者的 SamAccountName (登入名稱) 後面接 SIP 網域。例如，SamAccountName 為 room14 的使用者會有類似下列的 SIP 位址：room14@litwareinc.com。若您使用這種位址類型，還必須加入 SipDomain 參數。</p>
<p>如果您使用 SIPAddress 參數且明確指派 SIP 位址給使用者，則不需要 SipAddressType 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipDomain</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>要啟用之會議室的 SIP 網域。若您使用 SIPAddressType 參數讓 Lync Server 為使用者自動產生 SIP 位址，且您以 SamAccountName 或使用者的名字和姓氏做為 SIP 位址的基礎，則需要此參數。若您以使用者的電子郵件地址或 UPN 做為 SIP 位址的基礎，則不需要此參數；因為這些屬性值中已包含網域名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Enable-CsMeetingRoom** Cmdlet 接受管線傳送的字串值，該值代表已經針對 Lync Server 啟用的使用者帳戶 Identity。此 Cmdlet 也接受管線傳送的 Active Directory 使用者物件執行個體。

## 傳回類型

**Enable-CsMeetingRoom** Cmdlet 會建立 Microsoft.Rtc.Management.ADConnect.Schema.OCSADMeetingRoom 物件的新執行個體。

## 請參閱

#### 其他資源

[Disable-CsMeetingRoom](disable-csmeetingroom.md)  
[Get-CsMeetingRoom](get-csmeetingroom.md)  
[Move-CsMeetingRoom](move-csmeetingroom.md)  
[Set-CsMeetingRoom](set-csmeetingroom.md)

