---
title: Get-CsExUmContact
TOCTitle: Get-CsExUmContact
ms:assetid: 9c7b2afb-4d7f-4b5a-99dd-6f8978dd5728
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412725(v=OCS.15)
ms:contentKeyID: 49291803
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsExUmContact

 

_**上次修改主題的時間：** 2015-03-09_

擷取一或多個代管的 Exchange 整合通訊 (UM) 連絡人物件。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsExUmContact [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## 範例

## 範例 1

此範例會擷取 Lync Server 部署內定義的所有 Exchange UM 連絡人。

    Get-CsExUmContact

## 範例 2

此範例會擷取 SIP 位址為 sip:exum1@fabrikam.com 的 Exchange UM 連絡人

    Get-CsExUmContact -Identity sip:exum1@fabrikam.com

## 範例 3

在此範例中，我們使用 Filter 參數擷取未啟用 Lync Server 的所有 Exchange UM 連絡人。作法是篩選 Enabled 屬性，以查看此屬性的值是否等於 (-eq) False ($False)。此命令傳回的連絡人將沒有作用。

    Get-CsExUmContact -Filter {Enabled -eq $False}

## 範例 4

此命令會篩選 LineURI 屬性以擷取 LineURI 開頭為 tel:555 的所有 Exchange UM 連絡人。換言之，它會擷取電話號碼開頭為 555 的所有連絡人。

    Get-CsExUmContact -Filter {LineURI -like "tel:555*"}

## 範例 5

此範例中的命令使用 OU 參數來擷取 Active Directory OU OU=ExUmContacts,DC=Vdomain,DC=com 中的所有 Exchange UM 連絡人。

    Get-CsExUmContact -OU "OU=ExUmContacts,DC=Vdomain,DC=com"

## 詳細描述

Lync Server 搭配 Exchange UM 一起提供多項語音相關功能，包括「自動語音應答」和「使用者存取」。以主控服務 (非內部部署) 形式提供 Exchange UM 時，必須使用 Windows PowerShell 建立連絡人物件以套用「自動語音應答」和「使用者存取」功能。此 Cmdlet 會擷取其中一或多個連絡人。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsExUmContact** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsExUmContact"}

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
<td><p>可讓您以替代認證來執行 Cmdlet；如果您用來登入 Windows 的帳戶不具有使用連絡人物件所需的權限，可能就需要這一項。</p>
<p>若要使用 Credential 參數，您必須先呼叫 <strong>Get-Credential</strong> Cmdlet 建立 PSCredential 物件。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以擷取連絡人資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-mcs-001) 或其完整網域名稱 (例如，atl-mcs-001.litwareinc.com)。</p>
<p>完整資料類型：Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選 Lync Server 的相關屬性，以限制傳回的資料。例如，您可以將傳回的資料限制在線路 URI 開頭為 &quot;tel:555&quot; 的連絡人。</p>
<p>Filter 參數會使用 <strong>Where-Object</strong> Cmdlet 所使用之 Windows PowerShell 篩選語法的子集。例如，只傳回已啟用 Enterprise Voice 之連絡人的篩選看起來如下：{EnterpriseVoiceEnabled -eq $True}，其中 EnterpriseVoiceEnabled 代表 Active Directory 屬性；-eq 代表比較運算子 (等於)；$True (內建的 Windows PowerShell 變數) 代表篩選值。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>您要擷取之連絡人物件的唯一識別碼。可以使用下列四種格式的其中一種來指定連絡人識別身分：1) 連絡人的 SIP 位址；2) 連絡人的使用者主體名稱 (UPN)；3) 連絡人的網域名稱和登入名稱，必須是「網域\登入」格式 (例如，litwareinc\exum1)；以及 4) 連絡人的 Active Directory 顯示名稱 (例如，Team Auto Attendant)。</p>
<p>完整資料類型：Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選「一般」Active Directory 屬性 (也就是非 Lync Server 專屬的屬性)，以限制傳回的資料。</p>
<p>在建立篩選時，LdapFilter 參數會使用 LDAP 查詢語言。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>可讓您將擷取的資料限制在特定 Active Directory 組織單位 (OU)。請注意，這會從指定的 OU 及任何子 OU 傳回資料。</p>
<p>指定 OU 時，請使用該容器的辨別名稱；例如，OU=ExUmContacts,dc=litwareinc,dc=com。</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>可讓您限制命令傳回的記錄數。例如，若只要傳回七個連絡人 (不考慮樹系中有多少連絡人)，只需加入 ResultSize 參數並將參數值設為 7。請注意，無法保證傳回哪七個連絡人。如果您將 ResultSize 設為 7，但樹系中只有三個連絡人，則命令會傳回這三個連絡人，然後完成執行而不會出現錯誤。</p>
<p>結果大小可以設為 0 和 2147483647 (含) 之間的任何數字。如果設為 0，命令會執行，但不會傳回資料。</p>
<p>完整資料類型：Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。接受管線傳送的字串值，代表 Exchange UM 連絡人物件的 Identity。

## 傳回類型

傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact 類型的物件。

## 請參閱

#### 其他資源

[New-CsExUmContact](new-csexumcontact.md)  
[Remove-CsExUmContact](remove-csexumcontact.md)  
[Set-CsExUmContact](set-csexumcontact.md)  
[Move-CsExUmContact](move-csexumcontact.md)

