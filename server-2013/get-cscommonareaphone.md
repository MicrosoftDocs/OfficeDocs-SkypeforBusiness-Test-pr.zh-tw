---
title: Get-CsCommonAreaPhone
TOCTitle: Get-CsCommonAreaPhone
ms:assetid: bfb7927b-49a7-4637-a9ff-fd68897efb45
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412934(v=OCS.15)
ms:contentKeyID: 49292189
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCommonAreaPhone

 

_**上次修改主題的時間：** 2015-03-09_

傳回使用 Lync Server 管理之公用區電話的資訊。公共區域電話是位於大樓大廳、員工休息室，或其他可能由許多不同人使用之區域內的電話，用途可能各異。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsCommonAreaPhone [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有公用區電話的資訊。為達成此目的，可呼叫不含任何參數的 **Get-CsCommonAreaPhone** Cmdlet。

    Get-CsCommonAreaPhone

## 範例 2

範例 2 會傳回 Active Directory 顯示名稱為 "Building 14 Lobby" 的公用區電話。作法是加入 Filter 參數和篩選值 {DisplayName -eq "Building 14 Lobby"}；此篩選值會將傳回的物件限制為 DisplayName 屬性等於 "Building 14 Lobby" 的公用區電話。

    Get-CsCommonAreaPhone -Filter {DisplayName -eq "Building 14 Lobby"}

## 範例 3

範例 3 會傳回 Active Directory 顯示名稱是以字元 "Building 14" 開頭的所有公用區電話。為達成此目的，會呼叫 **Get-CsCommonAreaPhone** Cmdlet 搭配 Filter 參數，並使用篩選值 {DisplayName -like "Building 14\*"}。篩選值會使用 -like 運算子和萬用字元字串 "Building 14\*"，將傳回的資料限制在 DisplayName 屬性是以 "Building 14" 開頭的電話 (例如，"Building 14 Lobby"、"Building 14 Cafeteria" 等)。

    Get-CsCommonAreaPhone  -Filter {DisplayName -like "Building 14*"}

## 範例 4

範例 4 會傳回單一公用區電話：LineUri 屬性等於 "tel:+14255551234" 的電話。由於 LineUris 必須是唯一的，因此這個命令傳回的項目絕不會超過一個。

    Get-CsCommonAreaPhone  -Filter {LineUri -eq "tel:+14255551234"}

## 範例 5

範例 5 所示的命令會傳回所有未指派撥號對應表的公用區電話的資訊。作法是使用 Filter 參數和篩選值 {DialPlan -eq $Null}；這會將傳回資料限制為 DialPlan 屬性等 Null 值的電話。如果沒有明確指派撥號對應表給公用區電話，此電話會自動使用全域撥號對應表，或是指派撥號對應表 (如果有) 給該網站。

    Get-CsCommonAreaPhone -Filter {DialPlan -eq $Null}

## 範例 6

範例 6 傳回的集合是在 Active Directory 網域服務中的電信 OU 中有連絡人物件的所有公用區電話。作法是呼叫 **Get-CsCommonAreaPhone** Cmdlet 搭配 OU 參數；此參數值會將傳回的物件限制在辨別名稱為 ou=Telecommunications,dc=litwareinc,dc=com 的 OU 中具有連絡人物件的電話。

    Get-CsCommonAreaPhone -OU "ou=Telecommunications,dc=litwareinc,dc=com"

## 詳細描述

公用區電話是未與個別使用者相關聯的 IP 電話。公用區電話不是位於某個人的辦公室中，通常是位於建築物大廳、餐廳、員工休息室、會議室以及其他一群人可能聚集的地點。這對系統管理員而言是一個管理上的挑戰；這是因為在 Lync Server 中使用的電話通常是靠各種語音原則和撥號對應表在維護，而原則和對應表是指派給個別使用者。公用區電話不會被指派個別使用者。

解決此難題的方法是，針對所有的公用區電話建立 Active Directory 連絡人物件。(使用 **New-CsCommonAreaPhone** Cmdlet 建立這些連絡人物件)。就像使用者帳戶一樣，可以指派原則和語音對應表給這些連絡人物件。這樣一來，您就能夠對公用區電話保持控制，即使這些電話與個別使用者無關聯。例如，如果不要讓人從公用區電話轉接或保留通話，唯一要做的就是建立禁止通話轉接和保留通話的語音原則，然後將原則指派給公用區電話。(或者，更正確的說法是指派給代表公用區電話的連絡人物件)。例如，這個命令會指派語音原則 CommonAreaPhoneVoicePolicy 給您所有的公用區電話：

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

**Get-CsCommonAreaPhone** Cmdlet 提供一個方法，讓您能夠擷取設定供組織使用之所有公用區電話的資訊。如果您呼叫不含任何參數的 **Get-CsCommonAreaPhone** Cmdlet，Cmdlet 會傳回所有公用區電話的資訊。選用參數提供不同的方法讓您篩選資訊；例如，您可以傳回在指定組織單位 (OU) 中有連絡人物件的所有公用區電話，或位於指定建築物中的所有連絡人物件。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsCommonAreaPhone** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。可以使用 **Grant-CsOUPermission** Cmdlet，為特定網站或特定 Active Directory OU 指派執行此 Cmdlet 的權限。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCommonAreaPhone"}

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
<td><p>讓您可以用替代認證執行 <strong>Get-CsCommonAreaPhone</strong> Cmdlet。如果您用來登入 Windows 的帳戶不具有使用連絡人物件所需的必要權限，可能就需要這一項。</p>
<p>若要使用 Credential 參數，您必須先使用 <strong>Get-Credential</strong> Cmdlet 來建立 PSCredential 物件。如需詳細資訊，請參閱 <strong>Get-Credential</strong> Cmdlet 說明主題。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以擷取連絡人資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上該電腦的完整網域名稱 (FQDN) (如 atl-cs-001.litwareinc.com)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選 Lync Server 特定屬性來限制傳回的資料。例如，您可以將傳回的資料限制於已指派特定語音原則的公用區電話連絡人物件，或未指派特定語音原則的連絡人。</p>
<p>Filter 參數使用的 Windows PowerShell 篩選語法與 <strong>Where-Object</strong> Cmdlet 相同。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>公用區電話的唯一識別碼。識別公用區電話要使用相關聯連絡人物件的 Active Directory 辨別名稱 (DN)。根據預設，公用區電話會使用全域唯一識別碼 (GUID) 做為其一般名稱，這表示這類電話的 Identity 通常會如下所示：CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com。</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選一般 Active Directory 屬性 (也就是非 Lync Server 專屬的屬性)，以限制傳回的資料。例如，您可以將傳回的資料限制在已指派特定部門或位於特定建築物的連絡人物件。</p>
<p>在建立篩選時，LdapFilter 參數會使用 LDAP 查詢語言。例如，只傳回代表 Redmond 城市公用區電話的連絡人物件的篩選器如下所示：</p>
<p>-LDAPFilter &quot;l=Redmond&quot;</p>
<p>在上述篩選中，&quot;l&quot; (小寫的 L) 代表 Active Directory 屬性 (位置)，&quot;=&quot; 代表比較運算子 (等於)，而 &quot;Redmond&quot; 代表篩選值。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>可讓您從特定 Active Directory 組織單位 (OU) 傳回連絡人物件。OU 參數會從指定的 OU 及其任何子 OU 傳回資料。例如，如果 Finance OU 有兩個子 OU -- AccountsPayable 和 AccountsReceivable -- 則會從這三個 OU 中的每一個 OU 傳回共同的區域電話資訊。</p>
<p>指定 OU 時，請使用該容器的辨別名稱；例如：-OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>可讓您限制命令傳回的記錄數。例如，若只要傳回七個公用區電話 (不考慮樹系中有多少公用區電話)，請加入 ResultSize 參數並將參數值設為 7。請注意，無法保證傳回哪七個電話。如果您將 ResultSize 設為 7，但樹系中只有三個公用區電話，則命令會傳回這三個電話，然後完成執行而不會出現錯誤。</p>
<p>結果大小可以設為 0 和 2147483647 (含) 之間的任何數字。如果設為 0，命令會執行，但不會傳回資料。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。**Get-CsCommonAreaPhone** Cmdlet 接受代表公用區電話之 Identity 的管線傳送字串值。

## 傳回類型

**Get-CsCommonAreaPhone** Cmdlet 會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact 物件的執行個體。

## 請參閱

#### 其他資源

[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

