---
title: Get-CsOnlineUser
TOCTitle: Get-CsOnlineUser
ms:assetid: 2bfafd70-a7d9-4308-a353-5ecf44249b53
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994026(v=OCS.15)
ms:contentKeyID: 52056083
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsOnlineUser

 

_**上次修改主題的時間：** 2015-03-09_

傳回在 Microsoft Lync Online 上擁有帳戶之使用者的相關資訊。此 Cmdlet 僅可與 商務用 Skype Online 搭配使用。

## 語法

    Get-CsOnlineUser [[-Identity] <UserIdParameter>] [-Filter <String>] [-LdapFilter <String>] [-OnOfficeCommunicationServer] [-OnLyncServer] [-UnAssignedUser] [-OU <OUIdParameter>] [-DomainController <Fqdn>] [-Credential <PSCredential>] [-ResultSize <Unlimited`1>] [-Verbose]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定為線上使用者之所有使用者的資訊。

    Get-CsOnlineUser

## 範例 2

範例 2 會傳回單一線上使用者的資訊：SIP 位址為 "sip:kenmyer@litwareinc.com" 的使用者。

    Get-CsOnlineUser -Identity "sip:kenmyer@litwareinc.com"

## 範例 3

範例 3 所示的命令會傳回已針對 Lync Online 啟用但目前未指派給登錄器集區之所有線上使用者的資訊。

    Get-CsOnlineUser -UnassignedUser

## 範例 4

範例 4 會使用 Filter 參數，將傳回的資料限制為已指派有個別使用者封存原則 RedmondArchiving 的線上使用者。為達成此目的，會利用篩選值 {ArchivingPolicy -eq "RedmondArchiving"}。該語法會將傳回的資料限制為 ArchivingPolicy 屬性等於 (-eq) "RedmondArchiving" 的使用者。

    Get-CsOnlineUser -Filter {ArchivingPolicy -eq "RedmondArchiving"}

## 範例 5

範例 5 只會傳回已設定不會出現在 Microsoft Exchange 位址清單中 (也就是 Active Directory 屬性 msExchHideFromAddressLists 為 True) 之使用者帳戶的資訊。為達此目的，會一起加入 Filter 參數與篩選值 {HideFromAddressLists -eq $True}。

    Get-CsOnlineUser -Filter {HideFromAddressLists -eq $True}

## 範例 6

範例 6 所示的命令會傳回指派給 TenantID 為 "bf19b7db-6960-41e5-a139-2aa373474354" 之租用戶的所有線上使用者的相關資訊。為達此目的，命令會一起加入 Filter 參數與篩選值 {TenantId –eq "bf19b7db-6960-41e5-a139-2aa373474354"}。此篩選會將傳回的資料限制為指派到租用戶 "bf19b7db-6960-41e5-a139-2aa373474354" 的線上使用者。

    Get-CsOnlineUser -Filter {TenantId -eq "bf19b7db-6960-41e5-a139-2aa373474354"}

## 詳細描述

**Get-CsOnlineUser** Cmdlet 會傳回在 Microsoft Lync Online 上擁有帳戶之使用者的相關資訊。傳回的資訊包含標準 Active Directory 帳戶資訊 (例如使用者工作的部門、其地址和電話號碼等)，以及 Lync Server 特定資訊：**Get-CsOnlineUser** Cmdlet 會傳回是否已針對 Enterprise Voice 啟用使用者，及是否已將個別使用者原則 (若有的話) 指派給使用者之類的資訊。

請注意，**Get-CsOnlineUser** Cmdlet 沒有 TenantId 參數，這表示您無法使用與此命令類似的命令，不能將傳回的資料限制為擁有特定 Lync Online 租用戶之帳戶的使用者：

    Get-CsOnlineUser -TenantId "bf19b7db-6960-41e5-a139-2aa373474354"

不過，若有多個 Lync Online 租用戶，您可以使用 Filter 參數和以下的類似命令，從指定的租用戶傳回使用者：

    Get-CsOnlineUser -Filter {TenantId -eq "bf19b7db-6960-41e5-a139-2aa373474354"}

該命令會將傳回的資料限制在 TenantId 為 "bf19b7db-6960-41e5-a139-2aa373474354" 之租用戶的使用者帳戶。如果不知道租用戶識別碼，可使用此命令傳回該資訊：

    Get-CsTenant

如果您有混合式或「分割網域」部署 (也就是在此部署中，其中部分使用者擁有 Lync Online 帳戶，其他使用者則在內部部署版本的 Lync Server 上擁有帳戶)，請注意，**Get-CsOnlineUser** Cmdlet 只會傳回 Lync Online 使用者的資訊。不過，[Get-CsUser](get-csuser.md) Cmdlet 將傳回 Lync Online 使用者和內部部署 Lync Server 使用者二者的資訊。如果您希望 **Get-CsUser** Cmdlet 不要傳回 Lync Online 使用者的資料，請使用下列命令：

    Get-CsUser -Filter {TenantId -eq "00000000-0000-0000-0000-000000000000"}

依據定義，內部部署版本之 Lync Server 上的使用者一律會擁有等於 00000000-0000-0000-0000-000000000000 的 TenantId。Lync Online 上使用者的 TenantId 則是 00000000-0000-0000-0000-000000000000 以外的某個值。

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
<td><p>可讓您以替代認證來執行 <strong>Get-CsOnlineUser</strong> Cmdlet。如果您用來登入 Windows 的帳戶不具有使用使用者物件所需的必要權限，可能就需要這一項。</p>
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
<td><p>可讓您篩選 Lync Server 特定屬性來限制傳回的資料。例如，您可以將傳回的資料限制為已指派或未指派特定語音原則的使用者。</p>
<p>Filter 參數會使用 Where-Object Cmdlet 所使用的相同 Windows PowerShell 篩選語法。例如，下列篩選僅傳回已針對 Enterprise Voice 啟用的使用者，EnterpriseVoiceEnabled 代表 Active Directory 屬性、-eq 代表比較運算子 (等於)，而 $True (內建 Windows PowerShell 變數) 代表篩選值：</p>
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
<td><p>傳回舊版 Lync Server (例如 Microsoft Office Communications Server 2007 R2) 所屬之使用者的集合。當您使用此參數時，將不會傳回具有目前軟體版本之帳戶的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>可讓您傳回特定組織單位 (OU) 或容器中的使用者帳戶相關資訊。OU 參數會從指定的 OU 及其任何子 OU 傳回資料。例如，如果 Finance OU 有兩個子 OU (AccountsPayable 和 AccountsReceivable)，則會從這三個 OU 中的每一個 OU 傳回使用者。</p>
<p>指定 OU 時，請使用該容器的辨別名稱 (DN)，例如 -OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;。若要從 Users 容器傳回使用者帳戶，請採用此語法：</p>
<p>-OU &quot;cn=Users,dc=litwareinc,dc=com&quot;</p></td>
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
<td><p>可讓您傳回已針對 Lync Online 啟用但目前未指派到登錄器集區之所有使用者的集合。除非將使用者指派到登錄器集區，否則他們將無法登入。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Get-CsOnlineUser** Cmdlet 接受以管道方式傳送的 Microsoft.Rtc.Management.ADConnect.Schema.OCSADUser 物件執行個體，以及代表有效使用者帳戶 Identity 的字串值 (例如 "sip:kenmyer@litwareinc.com")。

## 傳回類型

**Get-CsOnlineUser** Cmdlet 會傳回 Microsoft.Rtc.Management.ADConnect.Schema.ADOCOnlineUser 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsUser](get-csuser.md)

