---
title: Get-CsEffectivePolicy
TOCTitle: Get-CsEffectivePolicy
ms:assetid: 03b2984f-3a24-4b8d-bcaf-5049de9e2556
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204636(v=OCS.15)
ms:contentKeyID: 49289933
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsEffectivePolicy

 

_**上次修改主題的時間：** 2015-03-09_

傳回一位或多位指定使用者的「有效原則」。這表示使用者若獲指派個別使用者原則，將會顯示該原則的 Identity。否則，**Get-CsEffectivePolicy** Cmdlet 將會指出使用者是由服務原則、網站原則或全域原則所管理。這可讓您明確地判斷管理指定使用者所使用的原則。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsEffectivePolicy -Identity <UserIdParameter> [-Credential <PSCredential>] [-DomainController <Fqdn>] [-ResultSize <Unlimited>]

## 範例

## 範例 1

範例 1 所示的命令會傳回 Active Directory 顯示名稱為 Ken Myer 之使用者的有效原則。

    Get-CsEffectivePolicy - Identity "Ken Myer"

## 範例 2

在上述命令中，會傳回顯示名稱為 Ken Myer 及 Pilar Ackerman 之使用者的有效原則資訊。您也可以管線傳送多個使用者 Identity 給 **Get-CsEffectivePolicy** Cmdlet，以傳回多位使用者的原則資訊。

    "Ken Myer","Pilar Ackerman" | Get-CsEffectivePolicy

## 範例 3

範例 3 傳回獲指派會議原則 RedmondConferencingPolicy 之所有使用者的有效原則資訊。為達成此目的，命令會先使用 **Get-CsUser** Cmdlet 傳回獲指派 RedmondConferencingPolicy 之使用者的集合；Filter 參數和 {ConferencingPolicy –eq "RedmondConferencingPolicy"} 篩選值會將傳回的資料限制在獲指派 RedmondConferencingPolicy 個別使用者會議原則的使用者。然後再將該使用者帳戶集合管線傳送到 **Get-CsEffectivePolicy** Cmdlet，以顯示集合中每位使用者的有效原則資訊。

    Get-CsUser -Filter {ConferencingPolicy -eq "RedmondConferencingPolicy"} | Get-CsEffectivePolicy

## 範例 4

範例 4 是範例 3 所示命令的變化。此範例會再一次傳回獲指派會議原則 RedmondConferencingPolicy 之所有使用者的有效原則資訊，但此範例只會傳回使用者 Identity 與行動原則的相關資訊。作法是先傳回所有有效的原則資訊，再將該資料管線傳送到 **Select-Object** Cmdlet，最後再使用此 Cmdlet 只顯示 Identity 和 MobilityPolicy 屬性的資料。

    Get-CsUser -Filter {ConferencingPolicy -eq "RedmondConferencingPolicy"} | Get-CsEffectivePolicy | Select-Object Identity, MobilityPolicy

## 範例 5

範例 5 會顯示財務部門中所有使用者的有效原則資訊。執行此工作的方法是先使用 **Get-CsUser** Cmdlet 和 LdapFilter 屬性傳回使用者帳戶的集合；篩選值 "Department=Finance" 會將帳戶限制在財務部門中工作的使用者。然後，此集合會管線傳送到 **Get-CsEffectivePolicy** Cmdlet，以顯示集合中每位使用者的有效原則資訊。

    Get-CsUser -LdapFilter "Department=Finance" | Get-CsEffectivePolicy

## 詳細描述

除此之外，**Get-CsUser** Cmdlet 會傳回用以管理使用者行為之 Microsoft Lync Server 原則的相關資訊。例如：

DialPlan : RedmondDialPlan

LocationPolicy : RedmondLocationPolicy

ClientPolicy :

在前面的輸出中，使用者看似由特定的撥號對應表與位原則所管理，而不是由用戶端所管理。事實上，使用者是由用戶端原則 (全域原則或網站原則) 所管理。但 **Get-CsUser** 只會傳回指派給使用者之個別使用者原則的相關資訊。對於全域原則、網站原則或服務原則所管理的使用者，**Get-CsUser** Cmdlet 不會傳回任何資訊。

在進行疑難排解時，知道使用者是由全域原則、網站原則或服務原則所管理十分實用。因為如此一來，您就可以使用 **Get-CsEffectivePolicy** Cmdlet 傳回用以管理使用者行為之原則的正確資訊。對於前述使用者，**Get-CsEffectivePolicy** Cmdlet 可能會傳回類似下列的資訊：

LocationProfile : RedmondDialPlan

LocationPolicy : RedmondLocationPolicy

ClientPolicy : Global

此輸出讓您知道該使用者受全域用戶端原則所管理。

請注意，**Get-CsEffectivePolicy** Cmdlet 和 **Get-CsUser** Cmdlet 不同，只會傳回原則的資訊，而不會傳回像使用者電話號碼、登錄器集區等的其他資訊。此外，**Get-CsUser** Cmdlet 與 **Get-CsEffectivePolicy** Cmdlet 命名原則時所用的術語也不相同。例如 **Get-CsUser** Cmdlet 會使用名稱 DialPlan，而 **Get-CsEffectivePolicy** Cmdlet 則會使用名稱 LocationProfile。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsEffectivePolicy"}

**Lync Server 控制台：在** Lync Server 控制台不提供 **Get-CsEffectivePolicy** Cmdlet 所執行的功能。

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
<td><p>指出要計算有效原則設定之使用者帳戶的 Identity。使用者 Identity 可以使用下列其中一種格式加以指定：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。您也可以利用使用者的 Active Directory 辨別名稱來參考使用者帳戶。</p>
<p>使用「顯示名稱」做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，將會傳回所有顯示名稱結尾為 &quot; Smith&quot; 字串值的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>Credential</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>可讓您使用替代認證來執行 Get-CsEffectivePolicy Cmdlet。如果您用於登入 Windows 的帳戶不具有使用使用者物件所需的必要權限，就可能要此參數。</p>
<p>若要使用 Credential 參數，您必須先使用 <strong>Get-Credential</strong> Cmdlet 來建立 PSCredential 物件。如需詳細資訊，請參閱 <strong>Get-Credential</strong> Cmdlet 說明主題。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站擷取使用者資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，並緊接其後指定完整網域名稱 (FQDN)。例如：</p>
<p>-DomainController &quot;atl-dc-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>可讓您限制 Cmdlet 傳回的記錄數。例如，若要傳回七位使用者 (不考慮樹系中的使用者數目)，請加入 ResultSize 參數並將參數值設為 7。請注意，此法無法保證傳回哪七位使用者。</p>
<p>結果大小可以設為 0 到 2147483647 的任何整數。如果設為 0，將只會執行命令而不會傳回資料。如果將 ResultSize 設為 7，但樹系中只有三位使用者，則命令完成時將只會傳回這三位使用者，而且不會出現錯誤。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Get-CsEffectivePolicy** Cmdlet 接受管線傳送的字串值，代表已針對 Lync Server 啟用使用者帳戶的顯示名稱。此 Cmdlet 也接受管線傳送的 Active Directory 使用者物件執行個體。

## 傳回類型

**Get-CsEffectivePolicy** Cmdlet 會傳回 Microsoft.Rtc.Management.AD.Cmdlets.EffectivePolicies 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsUser](get-csuser.md)

