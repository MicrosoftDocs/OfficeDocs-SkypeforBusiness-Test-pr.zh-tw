---
title: Enable-CsUser
TOCTitle: Enable-CsUser
ms:assetid: 8ceed97b-e802-4844-b509-c6ca9619ec55
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398711(v=OCS.15)
ms:contentKeyID: 49291606
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsUser

 

_**上次修改主題的時間：** 2015-03-09_

針對 Lync Server 啟用一或多位使用者。除非先針對 Lync Server 啟用使用者帳戶，否則使用者無法使用 Lync 2013 或其他 Lync Server 用戶端。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Enable-CsUser -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-HostingProviderProxyFqdn <Fqdn>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-RegistrarPool <Fqdn>] [-SipAddress <String>] [-SipAddressType <FirstLastName | EmailAddress | UserPrincipalName | SAMAccountName | None>] [-SipDomain <Fqdn>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，**Enable-CsUser** Cmdlet 會啟用顯示名稱為 Pilar Ackerman 的使用者帳戶。此範例會將該使用者指派至登錄器集區 atl-cs-001.litwareinc.com，且 Lync Server 會使用該使用者的 SamAccountName (pilar) 並加上 SIP 網域 litwareinc.com，以自動產生 SIP 位址。

    Enable-CsUser -Identity "Pilar Ackerman" -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddressType SamAccountName  -SipDomain litwareinc.com

## 範例 2

範例 2 會針對 Lync Server 啟用屬於 Pilar Ackerman 的 Active Directory 使用者帳戶。為了針對 Lync Server 設定帳戶，**Enable-CsUser** Cmdlet 將搭配下列參數使用：Identity (識別要啟用的帳戶)；RegistrarPool (表示要裝載使用者的 Standard Edition Server 或 Enterprise Edition 前端集區)；以及 SipAddress (指定新使用者的 SIP 位址)。此範例會明確指派 SIP 位址，而非使用 Lync Server 自動產生位址。

    Enable-CsUser -Identity "Pilar Ackerman" -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddress "sip:pilar@litwareinc.com"

## 範例 3

在範例 3 中，在財務部門工作的所有使用者都會對 Lync Server 啟用其帳戶。為了執行此工作，會使用 **Get-CsAdUser** Cmdlet 並搭配 LdapFilter 參數，以傳回所有在財務部門工作的使用者集合。然後將該資訊管線傳送到 **Enable-CsUser** Cmdlet，以針對 Lync Server 啟用集合中的每個帳戶。

若要啟用帳戶，您必須指定該使用者的登錄器集區和 SIP 位址。在此範例中，使用 RegistrarPool 參數指定登錄器集區。不過，並未直接指派 SIP 位址。而是在命令中加上 SipAddressType 和 SipDomain 這兩個參數。也就是說，將自動為每一個帳戶產生新的 SIP 位址，此位址由使用者的 SamAccountName 和 SIP 網域名稱組成。例如，SamAccountName 為 kenmyer 的使用者會被指定 SIP 位址 sip:kenmyer@litwareinc.com。

    Get-CsAdUser -LdapFilter "department=Finance" | Enable-CsUser -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddressType SamAccountName  -SipDomain litwareinc.com

## 範例 4

範例 4 會啟用尚未對 Lync Server 啟用的所有 Active Directory 使用者。為達成此目的，會叫用 **Get-CsAdUser** Cmdlet 並搭配 Filter 參數。{Enabled -ne $True} 篩選可傳回所有尚未針對 Lync Server 啟用之使用者的集合。然後，此集合會管線傳送到 **Enable-CsUser** Cmdlet，以啟用每個帳戶，並將使用者指派至登錄器集區 atl-cs-001.litwareinc.com，且為每位使用者自動產生 SIP 位址。

    Get-CsAdUser -Filter {Enabled -ne $True} | Enable-CsUser -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddressType SamAccountName  -SipDomain litwareinc.com

## 詳細描述

使用者必須符合兩項需求，才能登入 Lync Server：必須具備有效的 Active Directory 網域服務帳戶，且必須對 Lync Server 啟用該帳戶。對 Lync Server 啟用使用者帳戶的方法之一是使用 **Enable-CsUser** Cmdlet。若要使用此 Cmdlet 對 Lync Server 啟用帳戶，您必須：1) 選取要啟用的帳戶；2) 選取帳戶的登錄器集區 (也就是主伺服器)；以及 3) 為帳戶指派 SIP 位址。Lync Server 可讓系統管理員選擇為使用者指派特定 SIP 位址，或是讓 Lync Server 為您建立 SIP 位址。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Enable-CsUser** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Enable-CsUser"}

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
<td><p>表示要啟用 Lync Server 之使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。您也可以利用使用者的 Active Directory 辨別名稱來參考使用者帳戶。</p>
<p>使用「顯示名稱」做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會傳回所有顯示名稱結尾為字串值 &quot; Smith&quot; 的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以啟用使用者帳戶。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-cs-001) 或其完整網域名稱 (FQDN) (例如，atl-cs-001.litwareinc.com)。</p></td>
</tr>
<tr class="even">
<td><p><em>HostingProviderProxyFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>此參數只能用於 Lync Online。請勿用於 Lync Server 的內部部署實作。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您透過管線傳遞代表已對 Lync Server 啟用之使用者帳戶的使用者物件。根據預設，<strong>Enable-CsUser</strong> Cmdlet 不會透過管線傳遞物件。</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>此參數只能用於 Lync Online。請勿用於 Lync Server 的內部部署實作。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPool</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>表示使用者的 Lync Server 帳戶將隸屬的登錄器集區。</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您為使用者指派特定的 SIP 位址。指定 SIP 位址時，請記得在位址開頭加上 &quot;sip:&quot;。這表示提供給 SipAddress 參數的值應該會類似：</p>
<p>sip:kenmyer@litwareinc.com</p>
<p>如果您使用 SipAddressType 參數以便讓 Lync Server 自動為使用者產生 SIP 位址，則不應使用 SipAddress 參數。</p>
<p>如果您正在嘗試同時啟用多個使用者，則無法使用 SipAddress 參數。而是必須使用 SipAddressType 參數，為這些使用者自動產生 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddressType</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.Cmdlets.AddressType</p></td>
<td><p>指示 Lync Server 自動為新使用者產生 SIP 位址。為了讓 Lync Server 自動產生 SIP 位址，您必須加上 SipAddressType 參數並使用下列其中一個參數值：</p>
<p>FirstLastName。SIP 位址是使用者的名字加句點，再加上使用者的姓氏和 SIP 網域。例如，使用者 Ken Myer 的 SIP 位址會類似：Ken.Myer@litwareinc.com。如果您使用這種位址類型，還必須加入 SipDomain 參數。</p>
<p>EmailAddress。使用者的電子郵件地址 (如 Active Directory 中定義) 會當做 SIP 位址使用。</p>
<p>UserPrincipalName。使用者的 UPN 用作 SIP 位址。</p>
<p>SamAccountName。SIP 位址是使用者的 SamAccountName (登入名稱) 加上 SIP 網域。例如，SamAccountName 為 kmyer 的使用者會有如下的 SIP 位址：kmyer@litwareinc.com。如果您使用這種位址類型，還必須加入 SipDomain 參數。</p>
<p>如果您使用 SIPAddress 參數且明確指派 SIP 位址給使用者，則不需要 SipAddressType 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>SipDomain</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>要啟用之使用者帳戶的 SIP 網域。如果您使用 SIPAddressType 參數讓 Lync Server 自動為使用者產生 SIP 位址，且您以 SamAccountName 或使用者的名字和姓氏做為 SIP 位址的基礎，則需要此參數。如果您以使用者的電子郵件地址或 UPN 做為 SIP 位址的基礎，則不需要此參數；因為這些屬性值中已包含網域名稱。</p></td>
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

字串或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Enable-CsUser** Cmdlet 接受管線傳送的字串值，該值代表已經針對 Lync Server 啟用的使用者帳戶 Identity。此 Cmdlet 也接受管線傳送的 Active Directory 使用者物件執行個體。

## 傳回類型

無。**Enable-CsUser** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件的執行個體。

## 請參閱

#### 其他資源

[Disable-CsUser](disable-csuser.md)  
[Get-CsUser](get-csuser.md)

