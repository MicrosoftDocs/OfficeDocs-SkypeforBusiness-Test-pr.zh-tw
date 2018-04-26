---
title: Get-CsUser
TOCTitle: Get-CsUser
ms:assetid: 06f36c53-3a5e-4e79-b4f2-8c1aa7e6bf71
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398125(v=OCS.15)
ms:contentKeyID: 49289987
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUser

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織中啟用 Lync Server 或舊版軟體 (例如 Microsoft Office Communications Server 2007 R2) 之所有使用者的資訊。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsUser [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OnLyncServer <SwitchParameter>] [-OnOfficeCommunicationServer <SwitchParameter>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>] [-UnassignedUser <SwitchParameter>]

## 範例

## 範例 1

上述範例會呼叫不含任何參數的 **Get-CsUser** Cmdlet，以傳回已啟用 Lync Server 或 Office Communications Server 之所有網域使用者的集合。

    Get-CsUser

## 範例 2

在範例 2 中， **Get-CsUser** Cmdlet 傳回已啟用 Lync Server 或 Office Communications Server 之所有網域使用者的集合。根據預設， **Get-CsUser** Cmdlet 會傳回非常大量的屬性和屬性值，其中有許多在特定情況下是沒有意義的。因此，在此範例中，擷取的資料會管線傳送至 **Format-Table** Cmdlet。 **Format-Table** Cmdlet 接著會使用 Property 參數來選取屬性 DisplayName、SipAddress 以及 EnterpriseVoiceEnabled，並將這些屬性及其值顯示在表格中。

    Get-CsUser | Format-Table -Property DisplayName, SipAddress, EnterpriseVoiceEnabled -AutoSize

## 範例 3

在範例 3 中，Identity 參數用於將傳回的資料限制為具有 Identity (在此情況下為顯示名稱) 為 Pilar Ackerman 的使用者帳戶。

    Get-CsUser -Identity "Pilar Ackerman"

## 範例 4

在範例 4 中，萬用字元 (\*) 是在指定使用者的 Identity 時使用。這樣會使 **Get-CsUser** Cmdlet 傳回 Identity 開頭為字串值 "Pilar" 的所有使用者。

    Get-CsUser -Identity "Pilar*"

## 範例 5

範例 5 所示的命令會傳回未被指派個別使用者語音原則之使用者的集合。為達成此目的，命令會使用 Filter 參數搭配篩選 VoicePolicy -eq "$Null。建構搭配 **Get-CsUser** Cmdlet 使用的篩選時，您需要指定屬性名稱 (VoicePolicy)，後面緊接著比較運算子 (在此範例中為 "eq"，也就是表示「等於」的比較運算子)。緊接著比較運算子的是您要測試的值。在此範例中，該值為 $Null，這是代表 Null 值的 Windows PowerShell 命令列介面 變數。

若要傳回確實已指派語音原則的使用者集合，請使用此命令：

Get-CsUser -Filter {VoicePolicy -ne $Null}

    Get-CsUser -Filter {VoicePolicy -eq $Null}

## 範例 6

範例 6 會使用 LdapFilter 參數，將傳回的資料限制為在財務部門工作的使用者。作法是使用 LDAP 篩選值 "Department=Finance"。

    Get-CsUser -LdapFilter "Department=Finance"

## 範例 7

範例 7 示範如何搭配 LdapFilter 參數使用 AND 查詢。此查詢 (使用 & 字元 "&" 表示 AND 查詢) 會指定兩個條件："Department=Finance" 及 "Title=Manager"。若是此查詢所傳回的使用者帳戶，兩個條件都必須為 true：使用者必須在財務部門工作，且必須是主管。

    Get-CsUser -LdapFilter "&(Department=Finance)(Title=Manager)"

## 範例 8

範例 8 所示的命令中，OR 查詢是 (以縱線符號 "|" 表示) 搭配 LdapFilter 參數使用。範例 7 所示的 AND 查詢中，兩個條件都必須為 true，才會傳回使用者帳戶。若為 OR 查詢，只有一個條件必須為 true，就會傳回帳戶。在此案例中，如果使用者是監督人或主管，就會傳回使用者帳戶。

    Get-CsUser -LdapFilter "|(Title=Supervisor)(Title=Manager)"

## 範例 9

範例 9 會傳回在 Finance OU 中具有帳戶之所有使用者的使用者帳戶資訊。

    Get-CsUser -OU "ou=Finance,ou=North America,dc=litwareinc,dc=com"

## 範例 10

範例 10 會傳回已啟用 Lync Server 或 Office Communications Server，但目前未指派到登錄器集區之所有使用者的集合。

    Get-CsUser -UnassignedUser

## 詳細描述

**Get-CsAdUser** Cmdlet 和 **Get-CsUser** Cmdlet 同時使用時，可讓您傳回關於所有 Active Directory 使用者帳戶的詳細資訊。 **Get-CsAdUser** Cmdlet 會傳回所有使用者帳戶的資訊，包括已啟用 Lync Server 或 Office Communications Server 的使用者，以及未啟用 Lync Server 或 Office Communications Server 的使用者。這與 **Get-CsUser** Cmdlet 不同，後者只會傳回其帳戶已啟用 Lync Server 或 Office Communications Server 之使用者的資訊。

雖然兩者間的功能有某些重疊，但 **Get-CsUser** Cmdlet 和 **Get-CsAdUser** Cmdlet 傳回的資訊類型不同。一般而言， **Get-CsUser** Cmdlet 會傳回與 Lync Server 特別有關的 Active Directory 屬性的值。例如， **Get-CsUser** Cmdlet 所傳回的資訊諸如已指派給使用者的 Lync Server 原則；線路統一資源識別元 (URI) 是否已指派給該使用者；以及使用者是否已啟用企業語音的詳細資訊。除非使用者已啟用 Lync Server，否則使用者帳戶不會包含這些屬性。

相較之下，**Get-CsAdUser** Cmdlet 傳回的是一般 Active Directory 屬性值，這些屬性為基本 Active Directory 使用者帳戶一部分，且不論使用者是否啟用 Lync Server 都會存在。例如，**Get-CsAdUser** Cmdlet 所傳回的資訊除了使用者的職稱之外，還包括如使用者工作的部門和組織，以及使用者的電話號碼與公司地址。

若要查看 **Get-CsUser** Cmdlet 傳回的完整屬性值清單，請在 Windows PowerShell 命令提示字元下輸入此命令：

Get-CsUser | Get-Member

**Get-CsUser** Cmdlet 提供多種方式，讓您篩選執行 Cmdlet 時實際傳回的使用者集合。例如，如果您不想要傳回所有 Lync Server 使用者帳戶，可以套用選用的參數 Filter 或 LdapFilter (這些參數互不相容斥：命令中如有使用 Filter，即不可再使用 LdapFilter，反之亦然)。Filter 參數可讓您將傳回的資料限制為符合指定之 Lync Server 條件的使用者。例如，您可以決定只傳回帳戶位於指定登錄器集區上的使用者，或只傳回已啟用企業語音的使用者。LdapFilter 參數可讓您將傳回的資料限制於符合以 Active Directory 為基礎之其他條件的使用者；例如，在所指定縣市工作的使用者、具有或沒有呼叫器的使用者，或具有指定之工作職稱的使用者。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsUser** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUser\\b"}

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
<td><p>可讓您以替代認證來執行 <strong>Get-CsUser</strong> Cmdlet。如果您用來登入 Windows 的帳戶不具有使用使用者物件所需的必要權限，可能就需要這一項。</p>
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
<td><p>可讓您篩選 Lync Server 特定屬性來限制傳回的資料。例如，您可以將傳回的資料限制於已指派或未指派特定語音原則的使用者。</p>
<p>Filter 參數使用的 Windows PowerShell 篩選語法與 <strong>Where-Object</strong> Cmdlet 使用的相同。例如，只傳回啟用 Enterprise Voice 之使用者的篩選看起來像這樣，EnterpriseVoiceEnabled 表示 Active Directory 屬性、-eq 表示比較運算子 (等於)，而 $True (內建 Windows PowerShell 變數) 表示篩選值：</p>
<p>{EnterpriseVoiceEnabled -eq $True}</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>表示要擷取之使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。您也可以利用使用者的 Active Directory 辨別名稱來參考使用者帳戶。</p>
<p>使用「顯示名稱」做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會傳回所有顯示名稱結尾為字串值 &quot; Smith&quot; 的使用者。</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選一般 Active Directory 屬性 (也就是非 Lync Server 專屬的屬性)，以限制傳回的資料。例如，您可以將傳回的資料限制於在特定部門工作的使用者，或具有指定主管或工作職稱的使用者。</p>
<p>在建立篩選時，LdapFilter 參數會使用 LDAP 查詢語言。例如，只傳回在 Redmond 市工作之使用者的篩選器如下所示：&quot;l=Redmond&quot;，其中 &quot;l&quot; (小寫的 L) 代表 Active Directory 屬性 (locality)；&quot;=&quot; 是比較運算子 (等於)；&quot;Redmond&quot; 是篩選值。</p></td>
</tr>
<tr class="even">
<td><p><em>OnLyncServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回 Lync Server 所屬之使用者的集合。當您使用此參數時，將不會傳回具有舊版軟體之帳戶的使用者。</p></td>
</tr>
<tr class="odd">
<td><p><em>OnOfficeCommunicationServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回舊版 Lync Server (例如 Office Communications Server 2007 R2) 所屬之使用者的集合。當您使用此參數時，將不會傳回具有目前軟體版本之帳戶的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>可讓您傳回特定組織單位 (OU) 或容器中的使用者帳戶相關資訊。OU 參數會從指定的 OU 及其任何子 OU 傳回資料。例如，如果 Finance OU 有兩個子 OU (AccountsPayable 和 AccountsReceivable)，則會從這三個 OU 中的每一個 OU 傳回使用者。</p>
<p>指定 OU 時，請使用該容器的辨別名稱 (DN)；例如：-OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;。若要從 Users 容器傳回使用者帳戶，請採用此語法：-OU &quot;cn=Users,dc=litwareinc,dc=com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>可讓您限制 Cmdlet 傳回的記錄數。例如，若要傳回七個使用者 (不考慮樹系中的使用者數目)，請加入 ResultSize 參數並將參數值設為 7。請注意，此法無法保證傳回哪七位使用者。</p>
<p>結果大小可以設為 0 和 2147483647 (含) 之間的任何數字。如果設為 0，命令會執行，但不會傳回資料。如果您將 ResultSize 設為 7，但樹系中只有三個使用者，則命令會傳回這三個使用者，然後完成執行而不會出現錯誤。</p></td>
</tr>
<tr class="even">
<td><p><em>UnassignedUser</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您傳回已啟用 Lync Server，但目前未指派到登錄器集區之所有使用者的集合。除非將使用者指派到登錄器集區，否則他們將無法登入 Lync Server。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。 **Get-CsUser** Cmdlet 接受代表已啟用 Lync Server 之使用者帳戶 Identity 的管線傳送字串值。

## 傳回類型

**Get-CsUser** Cmdlet 會傳回 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件的執行個體。

## 請參閱

#### 其他資源

[Disable-CsUser](disable-csuser.md)  
[Enable-CsUser](enable-csuser.md)  
[Get-CsAdUser](get-csaduser.md)  
[Move-CsUser](move-csuser.md)  
[Set-CsUser](set-csuser.md)

