---
title: Get-CsUserAcp
TOCTitle: Get-CsUserAcp
ms:assetid: de65eafe-e306-4ada-8509-9688e81491f9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398978(v=OCS.15)
ms:contentKeyID: 49292543
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUserAcp

 

_**上次修改主題的時間：** 2015-03-09_

傳回指派給使用者或使用者群組之音訊會議提供者的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsUserAcp [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-Filter <String>] [-LdapFilter <String>] [-ResultSize <Unlimited>]

## 範例

## 範例 1

範例 1 所示的命令會為您組織中的所有使用者傳回音訊會議提供者的資訊。

    Get-CsUserAcp

## 範例 2

範例 2 會傳回單一使用者的音訊會議提供者資訊：Identity 為 Ken Myer 的使用者。此範例會利用使用者的 Active Directory 顯示名稱來指定識別。

    Get-CsUserAcp -Identity "Ken Myer"

## 範例 3

範例 3 會傳回已至少指派一位音訊會議提供者之所有使用者的資訊。為達此目的，會加上 Filter 參數搭配篩選值 AcpInfo –ne $Null (此篩選值可將傳回的資料限制在 AcpInfo 屬性值不等於 Null 值的使用者)。若要傳回尚未指派音訊會議提供者之使用者的資訊，請使用下列篩選值：

{AcpInfo –eq $Null}

    Get-CsUserAcp -Filter {AcpInfo -ne $Null}

## 範例 4

範例 4 會傳回已指派給音訊會議提供者 Fabrikam ACP 之所有使用者的音訊會議提供者資訊。為了執行此工作，命令會先使用不含任何參數的 **Get-CsUserAcp** Cmdlet，以傳回組織中所有使用者的音訊會議提供者資訊。然後將此資訊管線傳送到 **Where-Object** Cmdlet，這會挑出 AcpInfo 屬性包含 (-match) 字串值 "Fabrikam ACP" 的所有使用者。

    Get-CsUserAcp | Where-Object {$_.AcpInfo -match "Fabrikam ACP"}

## 範例 5

範例 5 會顯示指派給使用者 Ken Myer 之音訊會議提供者的詳細資訊。為達成此目的，會先呼叫 **Get-CsUserAcp** Cmdlet，以傳回 Ken Myer 之音訊會議提供者的資訊。然後將此資料管線傳送到 **Select-Object** Cmdlet，以使用 ExpandProperty 參數展開 AcpInfo 屬性值。展開屬性值表示所有儲存於該值中的資訊皆會以易於閱讀的方式顯示。

    Get-CsUserAcp -Identity "Ken Myer" | Select-Object -ExpandProperty AcpInfo

## 詳細描述

音訊會議提供者是提供組織會議服務的第三方公司。總而言之，音訊會議提供者提供處於異地之使用者在未連接至公司網路或網際網路，可參與會議之語音部分的方法。音訊會議提供者通常會提供高階服務，例如現場翻譯、記錄及現場個別會議總機服務。

Lync Server 不允許與音訊會議提供者完全整合。**CsUserAcp** Cmdlet 讓系統管理員可設定電話號碼和密碼，以及設定在使用者排程會議時隨時可用於音訊會議提供者整合的其他資訊。但是，因為這些 Cmdlet 並非設計來供 Lync Server 的內部部署版本使用 (他們的主要目的是和 Lync Online 搭配使用)，所以，除了指派內容值之外，不會提供任何其他音訊會議提供者整合。

**Get-CsUserAcp** Cmdlet 可讓您傳回指派給使用者或使用者群組之音訊會議提供者的資訊。若要傳回單一使用者的音訊會議提供者資訊，只要加入 Identity 參數，接著加上要傳回其資訊之使用者的 Identity 即可。若要傳回多位使用者的資訊，您可以使用 LdapFilter 或 Filter 參數。LdapFilter 參數可讓您使用一般的 Active Directory 屬性 (例如，指定使用者帳戶資訊時的 Department 或 Title)；例如，參數值 "Title=Accountant" 會將傳回的資訊限制在工作職稱為 Accountant 的使用者。Filter 參數可讓您使用 Lync Server 特定的屬性 (例如，VoicePolicy 或 EnterpriseVoiceEnabled) 來篩選傳回的資料。例如，篩選值 {EnterpriseVoiceEnabled –eq $True} 會將 **Get-CsUserAcp** Cmdlet 傳回的使用者帳戶限制在已啟用企業語音的使用者。

或者，您可以呼叫不含任何參數的 **Get-CsUserAcp** Cmdlet，以傳回所有使用者的音訊會議提供者資訊。請注意，**Get-CsUserAcp** Cmdlet 會傳回您所有使用者的音訊會議提供者資訊，包括尚未啟用 Lync Server 的使用者。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsUserAcp** Cmdlet：RTCUniversalUserAdmins、RTCUniversalReadOnlyAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUserAcp"}

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
<td><p>可讓您以替代認證來執行 <strong>Get-CsUserAcp</strong> Cmdlet。如果您用來登入 Windows 的帳戶不具有使用連絡人物件所需的必要權限，可能就需要這一項。</p>
<p>若要使用 Credential 參數，您必須先使用 <strong>Get-Credential</strong> Cmdlet 來建立 PSCredential 物件。如需詳細資訊，請參閱 <strong>Get-Credential</strong> Cmdlet 說明主題。</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選 Lync Server 特定屬性來限制傳回的資料。例如，您可以將傳回的資料限制於已指派或未指派特定語音原則的使用者。</p>
<p>Filter 參數使用的 Windows PowerShell 篩選語法與 <strong>Where-Object</strong> Cmdlet 相同。例如，只傳回啟用 Enterprise Voice 之使用者的篩選看起來像這樣，EnterpriseVoiceEnabled 表示 Active Directory 網域服務 屬性、-eq 表示比較運算子 (等於)，而 $True (內建 Windows PowerShell 變數) 表示篩選值：</p>
<p>{EnterpriseVoiceEnabled -eq $True}</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>表示要擷取的使用者帳戶之 Identity。您可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\kenmyer)；4) 使用者的 Active Directory 網域服務 顯示名稱 (如 Ken Myer)。您也可以使用使用者的 Active Directory 辨別名稱來參考使用者帳戶。</p>
<p>使用「顯示名稱」做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回所有顯示名稱是以字串 &quot; Smith&quot; 結束的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>LdapFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選一般 Active Directory 屬性 (也就是非 Lync Server 專屬的屬性)，以限制傳回的資料。例如，您可以將傳回的資料限制於在特定部門工作的使用者，或具有指定主管或工作職稱的使用者。</p>
<p>在建立篩選時，LdapFilter 參數會使用 LDAP 查詢語言。例如，只傳回在 Redmond 市工作之使用者的篩選器如下所示：&quot;l=Redmond&quot;，其中 &quot;l&quot; (小寫的 L) 代表 Active Directory 屬性 (locality)；&quot;=&quot; 是比較運算子 (等於)；&quot;Redmond&quot; 是篩選值。</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>可讓您限制命令傳回的記錄數。例如，若要傳回七個使用者 (不考慮樹系中有多少使用者)，請加入 ResultSize 參數並將參數值設為 7。請注意，無法保證傳回哪 7 個使用者。如果您將 ResultSize 設為 7，但樹系中只有三個使用者，則命令會傳回這三個使用者，然後完成執行而不會出現錯誤。</p>
<p>結果大小可以設為 0 和 2147483647 (含) 之間的任何數字。如果設為 0，命令會執行，但不會傳回資料。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。**Get-CsUserAcp** Cmdlet 接受代表已啟用 Lync Server 之使用者帳戶 Identity 的管線傳送字串值。

## 傳回類型

**Get-CsUserAcp** Cmdlet 會傳回 Microsoft.Rtc.Management.ADConnect.Schema.ADUserAcp 物件的執行個體。

## 請參閱

#### 其他資源

[Remove-CsUserAcp](remove-csuseracp.md)  
[Set-CsUserAcp](set-csuseracp.md)

