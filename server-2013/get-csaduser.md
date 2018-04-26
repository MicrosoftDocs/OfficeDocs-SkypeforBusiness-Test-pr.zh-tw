---
title: Get-CsAdUser
TOCTitle: Get-CsAdUser
ms:assetid: 787f0ccf-3ac3-4a2b-8407-cff5e988b9b4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398592(v=OCS.15)
ms:contentKeyID: 49291386
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdUser

 

_**上次修改主題的時間：** 2015-03-09_

傳回 Active Directory 網域服務 中所有使用者帳戶的資訊，包括可以使用 Lync Server 的使用者帳戶，以及無法使用 Lync Server 的帳戶。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsAdUser [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LDAPFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## 範例

## 範例 1

範例 1 所示的命令會傳回 Active Directory 網域中所有使用者帳戶的集合。

    Get-CsAdUser

## 範例 2

在範例 2 中，**Get-CsAdUser** Cmdlet 會傳回 Pilar Ackerman 的使用者帳戶資訊。在此範例中，使用者的顯示名稱可用來指定其 Identity。

    Get-CsAdUser -Identity "Pilar Ackerman"

## 範例 3

範例 3 會傳回 Finance 組織單位中全部使用者的使用者帳戶資訊。為達此目的，必須將 OU 的 DN 傳遞給 OU 參數。

    Get-CsAdUser -OU "ou=Finance,dc=litwareinc,dc=com"

## 範例 4

範例 4 會傳回所有未啟用 Lync Server 或 Office Communications Server 的使用者。為達成此目的，**Get-CsAdUser** Cmdlet 會搭配 Filter 參數，將傳回的資料限制在 Enabled 屬性不等於 True 的使用者帳戶。此篩選會指示 **Get-CsAdUser** Cmdlet 只傳回未啟用 Lync Server 或 Office Communications Server 的使用者帳戶。擷取資料之後會將資訊管線傳送到 **Select-Object** Cmdlet，以指定唯一會實際顯示在畫面上的屬性 (此範例中為 DisplayName)。

    Get-CsAdUser -Filter {Enabled -ne $True} | Select-Object DisplayName

## 範例 5

在範例 5 中，LdapFilter 參數可用來將傳回的資料限制於在財務部門服務的使用者。作法是使用 LDAP 篩選值 "Department=Finance"。

    Get-CsAdUser -LdapFilter "Department=Finance"

## 詳細描述

**Get-CsAdUser** Cmdlet 會傳回 Active Directory 網域服務中所有使用者帳戶的資訊，包含已啟用及未啟用 Lync Server 的使用者帳戶。這不同於 **Get-CsUser** Cmdlet，後者只會傳回已啟用 Lync Server 或舊版軟體 (例如 Microsoft Office Communications Server 2007 R2) 之帳戶使用者的資訊。

雖然這兩個 Cmdlet 的部分功能重疊，但 **Get-CsAdUser** Cmdlet 和 **Get-CsUser** Cmdlet 在傳回的資訊類型上也有所不同。一般而言，**Get-CsUser** Cmdlet 會傳回與 Lync Server 特別有關的 Active Directory 屬性的值。例如，**Get-CsUser** Cmdlet 可告知您哪些 Lync Server 原則已指派給使用者；指派給該使用者的線路統一資源識別元 (URI)；並指出使用者是否已啟用企業語音。除非使用者已啟用 Lync Server，否則使用者帳戶不會包含這些屬性。

相反地，**Get-CsAdUser** Cmdlet 會傳回一般的 Active Directory 屬性值；換言之，它傳回的屬性資訊是有關基本 Active Directory 使用者帳戶的屬性，且不論使用者是否啟用 Lync Server 都會存在的屬性。例如，**Get-CsAdUser** Cmdlet 會傳回的資訊包括使用者所服務的部門和組織，以及工作職稱、電話號碼和公司地址。若要查看 **Get-CsAdUser** Cmdlet 傳回的完整屬性值清單，請在 Windows PowerShell 提示字元下輸入下列命令：

Get-CsAdUser | Get-Member

**Get-CsAdUser** Cmdlet 提供多種方式可篩選執行 Cmdlet 時所傳回的使用者集合。例如，如果您並不想查看所有的 Active Directory 使用者帳戶，您可以套用選用參數 Filter 或 LdapFilter。這些參數彼此互斥：如果您在命令中使用 Filter，則不能在該相同的命令中使用 LdapFilter，反之亦然。Filter 參數可讓您將傳回的資料限制於符合 Lync Server 特定屬性之指定條件的使用者。例如，您可以使用 Filter 參數傳回已啟用或未啟用 Lync Server 的使用者集合。LdapFilter 參數可讓您將傳回的資料限制於符合其他基於一般 Active Directory 屬性之條件的使用者；例如，在指定縣市工作的使用者、有或沒有呼叫器的使用者，或身為指定工作職稱的使用者。

有關 **Get-CsAdUser** Cmdlet 值得注意的一點是：雖然決定使用者是否已啟用 Lync Server 的 Enabled 屬性為 Boolean 值，但是此屬性實際上有三個有效值：

True。使用者已啟用 Lync Server。

False。使用者暫時停用其 Lync Server 帳戶。一般的作法是使用 **Set-CsUser** Cmdlet 並將 Enabled 參數設為 $False。

Null。使用者未啟用 Lync Server。

換句話說，如果您想傳回未啟用 Lync Server 的使用者清單，則必須使用傳回 Enabled 屬性為 Null 之所有使用者的命令：

Get-CsAdUser –Filter {Enabled –eq $Null}

相反地，下列命令僅傳回暫時停用 Lync Server 帳戶的使用者：

Get-CsAdUser –Filter {Enabled –eq $False}

當您執行上述命令時，不會傳回未啟用 Lync Server 的使用者。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsAdUser** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAdUser"}

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
<td><p>可讓您以替代認證來執行 <strong>Get-CsAdUser</strong> Cmdlet。如果您用來登入 Windows 的帳戶不具有使用使用者物件所需的必要權限，可能就需要這一項。</p>
<p>若要使用 Credential 參數，您必須先使用 <strong>Get-Credential</strong> Cmdlet 來建立 PSCredential 物件。如需詳細資訊，請參閱 <strong>Get-Credential</strong> Cmdlet 說明主題。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站擷取使用者資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上完整網域名稱 (FQDN) (如 atl-cs-001.litwareinc.com)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選 Lync Server 特定屬性來限制傳回的資料。</p>
<p>Filter 參數使用的 Windows PowerShell 篩選語法與 <strong>Where-Object</strong> Cmdlet 相同。例如，若篩選只傳回已啟用 Lync Server 的使用者，則會如下所示：{Enabled -ne $True}，其中 Enabled 代表 Active Directory 屬性，-ne 代表比較運算子 (不等於)；$True (內建的 Windows PowerShell 變數) 代表 True 值。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>表示要擷取的使用者帳戶之 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。您也可以利用使用者的 Active Directory 辨別名稱來參考使用者帳戶。</p>
<p>使用「顯示名稱」做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會傳回所有顯示名稱結尾為字串值 &quot; Smith&quot; 的使用者。</p></td>
</tr>
<tr class="odd">
<td><p><em>LDAPFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選一般 Active Directory 屬性 (也就是非 Lync Server 專屬的屬性)，以限制傳回的資料。例如，您可以將傳回的資料限制於在特定部門工作的使用者，或具有特定主管或工作職稱的使用者。</p>
<p>在建立篩選時，LdapFilter 參數會使用 LDAP 查詢語言。例如，只傳回在 Redmond 市工作之使用者的篩選器如下所示：&quot;l=Redmond&quot;，其中 &quot;l&quot; (小寫的 L) 代表 Active Directory 屬性 (locality)；&quot;=&quot; 是比較運算子 (等於)；&quot;Redmond&quot; 是篩選值。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>可讓您傳回特定 Active Directory 組織單位 (OU) 或容器的使用者。此參數會從指定的 OU 及其任何子 OU 傳回資料。例如，如果 Finance OU 有兩個子 OU (AccountsPayable 和 AccountsReceivable)，則會從這三個 OU 中的每一個 OU 傳回使用者。</p>
<p>指定 OU 時，請使用該容器的辨別名稱 (DN)；例如：OU=Finance,dc=litwareinc,dc=com。若要從使用者容器傳回使用者，請使用下列語法：cn=Users,dc=litwareinc,dc=com。</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>可讓您限制 Cmdlet 傳回的記錄數。例如，若要傳回 7 個使用者 (不考慮樹系中的使用者數目)，請加入 ResultSize 參數並將參數值設為 7。請注意，無法保證傳回哪 7 個使用者。</p>
<p>結果大小可以設為 0 和 2147483647 (含) 之間的任何數字。如果設為 0，命令會執行，但不會傳回資料。如果您將 ResultSize 設為 7，但樹系中只有三個使用者，則命令會傳回這三個使用者，然後完成執行而不會出現錯誤。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。**Get-CsAdUser** Cmdlet 會接受管線傳送的字串值，該值代表 Active Directory 使用者帳戶的 Identity。

## 傳回類型

**Get-CsAdUser** Cmdlet 會傳回 Microsoft.Rtc.Management.ADConnect.Schema.CSADUser 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsUser](get-csuser.md)

