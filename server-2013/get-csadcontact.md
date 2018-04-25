---
title: Get-CsAdContact
TOCTitle: Get-CsAdContact
ms:assetid: a5f599fb-8ede-432d-a6bf-c850c68fc71e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412776(v=OCS.15)
ms:contentKeyID: 49291903
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdContact

 

_**上次修改主題的時間：** 2015-03-09_

在多樹系拓撲中，會從主樹系以外之樹系中傳回使用者帳戶的相關資訊；有些使用者已透過 Microsoft Forefront Identity Manager 2010 (或舊版產品) 複寫為連絡人物件。 **Get-CsAdContact** Cmdlet 會傳回所有設有 msRTCSIP-OriginatorSid 屬性值的使用者。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsAdContact [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LDAPFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## 範例

## 範例 1

範例 1 所示的命令會傳回 Active Directory 網域服務中所有多樹系連絡人的集合。呼叫不含任何其他參數的 **Get-CsAdContact** Cmdlet，會傳回所有 Active Directory 連絡人的所有屬性值。

    Get-CsAdContact

## 範例 2

範例 2 也會傳回 Active Directory 所有連絡人的集合。但是在這個例子中，該集合會傳送給 **Select-Object** Cmdlet，由其指定會顯示在螢幕上的兩個屬性：DisplayName 和 SipAddress。

    Get-CsAdContact | Select-Object DisplayName, SipAddress

## 範例 3

範例 3 會傳回單一 Active Directory 連絡人的資訊：含有 Identity 為 "Ken Myer" 的連絡人。

    Get-CsAdContact -Identity "Ken Myer"

## 範例 4

在範例 4 中，命令會傳回所有為 Fabrikam 工作的 Active Directory 連絡人。為達成此目的，會呼叫 **Get-CsAdContact** Cmdlet 搭配 LdapFilter 參數。在此範例中，會將傳回的資料限制為 Organization 屬性設定為 "Fabrikam" 的連絡人。

    Get-CsAdContact -LdapFilter "Organization=Fabrikam"

## 範例 5

範例 5 中的兩個命令示範 Credential 參數的使用，此參數讓您可以用替代認證來執行 **Get-CsAdContact** Cmdlet。第一個命令會呼叫 **Get-Credential** Cmdlet 來建立 litwareinc\\administrator 帳戶的 PSCredential 物件。此命令會顯示使用者 litwareinc\\administrator 的 \[認證要求\] 對話方塊；在您提供此帳戶的密碼後，該認證資訊將會儲存於變數 $x 中。第二個命令會呼叫 **Get-CsAdContact** Cmdlet 搭配 Credential 參數。參數值 $x 表示 **Get-CsAdContact** Cmdlet 應該在 litwareinc\\administrator 帳戶下執行。

    $x = Get-Credential -Credential "litwareinc\administrator"
    Get-CsAdContact -Credential $x

## 詳細描述

在多樹系拓撲中，來自其他樹系的使用者是以連絡人表示。這些連絡人和 Active Directory 連絡人不一樣；如果您使用 \[Active Directory 使用者和電腦\] 建立新的連絡人， **Get-CsAdContact** Cmdlet 不會傳回該連絡人。而是 **Get-CsAdContact** Cmdlet 只會傳回來自您主樹系以外之樹系的使用者資訊。如果您沒有多樹系拓撲，則不必呼叫 **Get-CsAdContact** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsAdContact** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAdContact"}

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
<td><p>可讓您以替代認證來執行 <strong>Get-CsAdContact</strong> Cmdlet；如果您用來登入 Windows 的帳戶不具有使用連絡人物件所需的權限，可能就需要這一項。</p>
<p>若要使用 Credential 參數，必須先使用 <strong>Get-Credential</strong> Cmdlet 建立 PSCredential 物件。如需詳細資訊，請參閱說明主題＜Get-Credential＞。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以擷取連絡人資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上完整網域名稱 (如 atl-cs-001.litwareinc.com)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選 Lync Server 特定屬性來限制傳回的資料。</p>
<p>Filter 參數使用的 Windows PowerShell 篩選語法與 <strong>Where-Object</strong> Cmdlet 相同。例如，只會傳回 SIP 位址是以 &quot;fabrikam.com&quot; 結束之連絡人的篩選器看起來如下：{SipAddress -like &quot;*@fabrikam.com&quot;}，其中 SipAddress 代表 Active Directory 屬性、-like 代表比較運算子，而 &quot;*@fabrikam.com&quot; 代表篩選值。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>表示要傳回之連絡人的 Identity。可以使用下列三種格式中的其中一種來指定連絡人 Identity：1) 連絡人的 SIP 位址；2) 連絡人的 Active Directory 辨別名稱；以及 3) 連絡人的 Active Directory 顯示名稱 (例如 Ken Myer)。</p>
<p>使用「顯示名稱」做為連絡人 Identity 時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回顯示名稱以字串 &quot;Smith&quot; 結束的所有連絡人。</p></td>
</tr>
<tr class="odd">
<td><p><em>LDAPFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選一般 Active Directory 屬性來限制傳回的資料。例如，您可以將傳回的資料限制於在特定部門工作的連絡人，或具有指定主管或工作職稱的連絡人。</p>
<p>在建立篩選時，LdapFilter 參數會使用 LDAP 查詢語言。例如，傳回電話號碼為 1-425-555-1298 之連絡人的篩選器看起來如下：&quot;telephoneNumber=1-425-555-1298&quot;，其中 &quot;telephoneNumber&quot; 代表 Active Directory 屬性、&quot;=&quot; 代表比較運算子 (等於)，而 &quot;1-425-555-1298&quot; 代表篩選值。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>可讓您限制從特定 Active Directory 組織單位 (OU) 或容器擷取的資訊。此參數會從指定的 OU 及其任何子 OU 傳回資料。例如，如果 Finance OU 有兩個子 OU：會從這三個 OU 傳回 AccountsPayable 和 AccountsReceivable 連絡人。</p>
<p>指定 OU 時，請使用該容器的辨別名稱；例如：OU=Finance,dc=litwareinc,dc=com。</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>可讓您限制 Cmdlet 傳回的記錄數。例如，若要傳回 7 個連絡人 (不考慮樹系中的連絡人數目)，請加入 ResultSize 參數並將參數值設為 7。請注意，無法保證傳回哪 7 個使用者。</p>
<p>結果大小可以設為 0 和 2147483647 (含) 之間的任何數字。如果設為 0，命令會執行，但不會傳回資料。如果您將 ResultSize 設為 7，但樹系中只有三個連絡人，則命令會傳回這三個連絡人，然後完成執行而不會出現錯誤。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。 **Get-CsAdContact** Cmdlet 接受代表使用者帳戶之 Identity 的管線傳送字串值。

## 傳回類型

**Get-CsAdContact** Cmdlet 會傳回 Microsoft.Rtc.Management.ADConnect.Schema.ADContact 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsAdUser](get-csaduser.md)  
[Get-CsUser](get-csuser.md)

