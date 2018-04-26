---
title: Grant-CsLocationPolicy
TOCTitle: Grant-CsLocationPolicy
ms:assetid: f820f892-c247-447c-947a-00414189842e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413049(v=OCS.15)
ms:contentKeyID: 49292865
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsLocationPolicy

 

_**上次修改主題的時間：** 2015-03-09_

指派增強型 9-1-1 (E9-1-1) 位置原則給個別使用者或群組。E9-1-1 服務可協助接聽緊急電話的人員判別來電者的地理位置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Grant-CsLocationPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，**Grant-CsLocationPolicy** Cmdlet 會用來將 Reno 位置原則指派給使用者 Ken Myer。

    Grant-CsLocationPolicy -Identity "Ken Myer" -PolicyName Reno

## 範例 2

在範例 2 中，AccountingArea 原則已指派給位於 Accounting 部門的所有使用者。為了傳回 Accounting 部門中所有使用者的集合，會使用 **Get-CsUser** Cmdlet 搭配 LDAPFilter 參數。傳送給 LDAPFilter -- "Department=Accounting" -- 的查詢值會傳回 Active Directory Department 設定為 Accounting 的所有使用者。然後將此集合傳送到 **Grant-CsLocationPolicy** Cmdlet，這會繼續將 AccountingArea 原則指派給集合中的每位使用者。

    Get-CsUser -LDAPFilter "Department=Accounting" | Grant-CsLocationPolicy -PolicyName AccountingArea

## 範例 3

此範例會將位置原則 Reno 賦予 Identity (在此範例中為顯示名稱) 為 Ken Myer 的使用者。此外，範例會包含參數 PassThru，它將在賦予位置原則之後，顯示使用者 Ken Myer 的使用者資訊。但是，不會立即將使用者資訊顯示於主控台上，而是會將該資訊傳送到 **Select-Object** Cmdlet，它將只會顯示使用者的 DisplayName 和 LocationPolicy 屬性。

此範例中其中一個要注意的事項是，新賦予的位置原則將出現在 LocationPolicy 下方的輸出中，但將顯示為 Anchor 值，而非原則名稱 (Anchor 值是在原則建立時自動指派給它的數值)。若要查看所套用的原則名稱，請執行命令 Get-CsUser –Identity "Ken Myer" | Select-Object DisplayName, LocationPolicy。

    Grant-CsLocationPolicy -Identity "Ken Myer" -PolicyName Reno -PassThru | Select-Object DisplayName, LocationPolicy

## 詳細描述

位置原則可用來套用和 E9-1-1 功能相關的設定。位置原則會判斷使用者是否已啟用 E9-1-1，如果是，則會決定緊急電話的行為。例如，您可以使用位置原則來定義組成緊急電話的數字 (在美國為 911)、是否應自動告知公司的安全部門，以及應如何路由傳送來電。此 Cmdlet 會將位置原則賦予特定的使用者或群組。

重要：位置原則的行為在範圍順序方面與 Lync Server 中的其他原則不同。對於其他的所有原則，如果原則是在個別使用者範圍中定義，則該原則會套用至任何授與該原則的使用者。如果使用者尚未授與個別使用者原則，則會套用網站原則。如果沒有網站原則，則會套用全域原則。系統也會以相同方式套用位置原則，但有一例外：系統也會將個別使用者位置原則指派給網站 (網站由一組子網路構成)。如果使用者正從對應到組織內部網站的位置撥打緊急電話，則會使用指派給該網站的使用者層級原則。此功能會覆寫已經授與給該使用者的個別使用者原則。如果使用者從未知或組織中未對應的位置撥打電話，將會套用標準原則範圍。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Grant-CsLocationPolicy** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsLocationPolicy"}

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
<td><p>指出要將原則指派給哪一個使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。請注意，無法使用 SAMAccountName 做為識別身分。</p>
<p>此外，使用顯示名稱做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會將原則賦予姓氏為 Smith 的所有使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要套用至使用者之位置原則的 Identity。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>容許您指定網域控制站。若未指定網域控制站，則會使用第一個可用的網域控制站。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>包含此參數 (不會取得值) 會在 Cmdlet 完成時顯示使用者資訊。執行此 Cmdlet 時通常不會有輸出。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。接受代表使用者帳戶 (已被授與位置原則) 識別身分的管線字串值。

## 傳回類型

搭配 PassThru 參數使用時，會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADUserOrAppContact 類型的物件。

## 請參閱

#### 其他資源

[New-CsLocationPolicy](new-cslocationpolicy.md)  
[Remove-CsLocationPolicy](remove-cslocationpolicy.md)  
[Set-CsLocationPolicy](set-cslocationpolicy.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Test-CsLocationPolicy](test-cslocationpolicy.md)  
[Get-CsUser](get-csuser.md)

