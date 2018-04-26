---
title: Get-CsAdPrincipal
TOCTitle: Get-CsAdPrincipal
ms:assetid: df2c3714-4064-4113-861f-95ce0ae8da81
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205326(v=OCS.15)
ms:contentKeyID: 49292550
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdPrincipal

 

_**上次修改主題的時間：** 2015-03-09_

傳回 Active Directory 主體的資訊。這些主體包括使用者、群組、連絡人、容器及組織單位等 Active Directory 物件。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsAdPrincipal [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LDAPFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織中的所有 Active Directory 主體。

    Get-CsAdPrincipal

## 範例 2

範例 2 會傳回單一 Active Directory 主體的資訊：SIP 位址為 "sip:RedmondMeetingRoom@litwareinc.com" 的主體。為達此目的，加入了 Filter 參數和篩選值，以尋找 SipAddress 屬性等於 (-eq) "sip:RedmondMeetingRoom@litwareinc.com" 的主體。

    Get-CsAdPrincipal -Filter {SipAddress -eq "sip:RedmondMeetingRoom@litwareinc.com"}

## 範例 3

在上述範例中，會傳回所有 Active Directory 物件的資訊。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsAdPrincipal** Cmdlet，以傳回所有 Active Directory 主體的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 ObjectClass 屬性包含字串值 "contact" 的主體。

    Get-CsAdPrincipal | Where-Object {$_.ObjectClass -contains "contact"}

## 詳細描述

**Get-CsAdPrincipal** Cmdlet 會傳回建構常設聊天室成員資格清單時所使用之 Active Directory 主體的集合 (如需詳細資訊，請參閱 **Set-CsPersistentChatCategory** Cmdlet 之 AllowedMembers 與 DeniedMembers 參數的說明資訊)。**Get-CsPrincipal** 傳回的 Active Directory 物件資訊包括：

  - **Users** (object class = {top, person, organizationalPerson, user})

  - **Groups** (object class = {top, group})

  - **Contacts** (object class = {top, person, organizationalPerson, contact})

  - **Containers** (object class = {top, container})

  - **Organizational Units** (object class = {top, organizationalUnit})

  - **Domains** (object class = {top, domain, domainDNS})

這表示您可以使用 **Get-CsAdPrincipal** Cmdlet (搭配 objectClass 屬性) 快速傳回 Active Directory 物件 (例如群組或組織單位) 的資訊。例如，下列命令可以傳回所有 Active Directory OU 的名稱：

Get-CsAdPrincipal | Where-Object {$\_.ObjectClass –match "organizationalUnit"} | Select-Object Name

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAdPrincipal"}

**Lync Server 控制台：**Lync Server 控制台不提供 Get-CsAdPrincipal Cmdlet 所執行的功能。

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
<td><p><em>Credential</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>可讓您以替代認證來執行 <strong>Get-CsAdPrincipal</strong> Cmdlet。如果您用來登入 Windows 的帳戶不具有使用使用者物件所需的必要權限，可能就需要這一項。</p>
<p>若要使用 Credential 參數，您必須先使用 <strong>Get-Credential</strong> Cmdlet 來建立 PSCredential 物件。如需詳細資訊，請參閱 <strong>Get-Credential</strong> Cmdlet 說明主題。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以擷取 Active Directory 主體資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-dc-001) 或其完整網域名稱 (FQDN) (例如，atl-dc-001.litwareinc.com)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選 Lync Server 特定屬性來限制傳回的資料。</p>
<p>Filter 參數使用的 Windows PowerShell 篩選語法與 <strong>Where-Object</strong> Cmdlet 幾乎相同。例如，只傳回未針對 Lync Server 啟用之主體的篩選如下所示：</p>
<p>-Filter {Enabled -ne $True}</p>
<p>在此範例中，Enabled 代表 Active Directory 屬性，-ne 代表比較運算子 (不等於)，而 $True (內建的 Windows PowerShell 變數) 代表 True 值。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>表示要擷取之主體帳戶的 Identity。通常可以使用下列四種格式的其中一種來指定識別：1) 帳戶的 SIP 位址；2) 使用者的使用者主要名稱 (UPN)；3) 帳戶的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\kenmyer)；4) 帳戶的 Active Directory 顯示名稱 (例如 Ken Myer)。</p>
<p>您也可以利用使用者的 Active Directory 辨別名稱來參考使用者帳戶。</p>
<p>使用「顯示名稱」做為 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會傳回所有顯示名稱結尾為字串值 &quot; Smith&quot; 的使用者。</p></td>
</tr>
<tr class="odd">
<td><p><em>LDAPFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選一般 Active Directory 屬性 (也就是非 Lync Server 專屬的屬性)，以限制傳回的資料。例如，您可以將傳回的資料限制於屬於特定部門的主體，或具有特定主管或工作職稱的主體。</p>
<p>在建立篩選時，LdapFilter 參數會使用 LDAP 查詢語言。例如，只傳回位於 Redmond 市之主體的篩選如下所示：</p>
<p>-LdapFilter &quot;l=Redmond&quot;</p>
<p>在此範例中，&quot;l&quot; (小寫的 L) 代表 Active Directory 屬性 (位置)，&quot;=&quot; 代表比較運算子 (等於)，而 &quot;Redmond&quot; 代表篩選值。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>可讓您傳回特定組織單位 (OU) 或容器中的主體相關資訊。OU 參數會從指定的 OU 及其任何子 OU 傳回資料。例如，如果 Finance OU 有兩個子 OU (AccountsPayable 和 AccountsReceivable)，則會從這三個 OU 中的每一個 OU 傳回主體。</p>
<p>指定 OU 時，請使用該容器的辨別名稱 (DN)；例如：</p>
<p>-OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;</p>
<p>若要從使用者容器傳回主體，請使用下列語法：</p>
<p>-OU &quot;cn=Users,dc=litwareinc,dc=com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>可讓您限制 Cmdlet 傳回的記錄數。例如，若要傳回七個主體 (不考慮樹系中的主體數目)，請加入 ResultSize 參數並將參數值設為 7。請注意，無法保證傳回哪七個主體。</p>
<p>結果大小可以設為 0 和 2147483647 (含) 之間的任何數字。如果設為 0，命令會執行，但不會傳回資料。如果您將 ResultSize 設為 7，但樹系中只有三個主體，則命令會傳回這三個主體，然後執行完成而不會出現錯誤。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串值或代表 Active Directory 使用者、群組、連絡人、容器及組織單位的物件。例如，下列語法會傳回 Redmond 和 Dublin OU 的 Active Directory 主體資訊：

"OU=Redmond,DC=litwareinc,DC=com", "OU=Dublin,DC=litwareinc,DC=com" | Get-CsAdPrincipal

## 傳回類型

**Get-CsAdPrincipal** Cmdlet 會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADPrincipal 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsPersistentChatCategory](new-cspersistentchatcategory.md)  
[Set-CsPersistentChatCategory](set-cspersistentchatcategory.md)

