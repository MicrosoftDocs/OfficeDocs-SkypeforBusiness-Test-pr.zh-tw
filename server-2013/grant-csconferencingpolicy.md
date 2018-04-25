---
title: Grant-CsConferencingPolicy
TOCTitle: Grant-CsConferencingPolicy
ms:assetid: 43c63a01-5072-45f0-89ee-8c3ae0cd9035
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425937(v=OCS.15)
ms:contentKeyID: 49290756
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsConferencingPolicy

 

_**上次修改主題的時間：** 2015-03-09_

在個別使用者範圍指派會議原則。會議原則可指定會議中所能使用的功能，包括會議是否可以加入 IP 音訊和視訊，乃至於會議出席人數的上限等等。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Grant-CsConferencingPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，**Grant-CsConferencingPolicy** Cmdlet 用來將 SalesConferencingPolicy 原則指派給 Identity 為 "Ken Myer" 的使用者。

    Grant-CsConferencingPolicy -identity "Ken Myer" -PolicyName SalesConferencingPolicy

## 範例 2

在範例 2 中，會議原則 FinanceConferencingPolicy 會指派給在財務組織單位中擁有帳戶的所有使用者。若要將相同的原則指派給指定組織單位 (OU) 中的所有使用者，則要使用 **Get-CsUser** Cmdlet 擷取該 OU 中的所有帳戶。已擷取使用者帳戶之後，該資訊會傳送到 **Grant-CsConferencingPolicy** Cmdlet，以將 FinanceConferencingPolicy 原則指派給集合中的每位使用者。

    Get-CsUser -OU "ou=Finance,dc=litwareinc,dc=com" | Grant-CsConferencingPolicy -PolicyName FinanceConferencingPolicy

## 範例 3

範例 3 代表範例 2 的變化：但是在此情況下，先前指派給 Finance OU 使用者的任何個別使用者會議原則都會變成取消指派。為達成此目的，此命令會呼叫 **Grant-CsConferencingPolicy** Cmdlet 並指定 null 值 ($Null)，做為參數 PolicyName 的參數值。

    Get-CsUser -OU "ou=Finance,dc=litwareinc,dc=com" | Grant-CsConferencingPolicy -PolicyName $Null

## 範例 4

範例 4 會將原則 HRConferencingPolicy 指派給在人力資源部門中工作的所有使用者。作法是呼叫 **Get-CsUser** Cmdlet 和 LDAPFilter 參數以擷取一組適當的使用者；"Department=Human Resources" 參數值會將傳回的項目限制為 Department 屬性設為 "Human Resources" 的帳戶。擷取使用者帳戶之後，該集合會傳送到 **Grant-CsConferencingPolicy** Cmdlet，將原則 HRConferencingPolicy 指派給集合中的每位使用者。

    Get-CsUser -LdapFilter "Department=Human Resources" | Grant-CsConferencingPolicy -PolicyName HRConferencingPolicy

## 詳細描述

會議是 Lync Server 中十分重要的部分，其讓使用者群組可以共同在線上檢視投影片和視訊、共用應用程式、交換檔案，甚至進行通訊及共同作業。

對於系統管理員來說，最重要的是保有對於會議與會議設定的控制權。在某些情況下，可能會有安全性顧慮：預設任何人 (包括未驗證的使用者) 都可以參與會議，並儲存會議期間散佈的任何投影片或講義。在某些情況下，可能會有頻寬顧慮：有許多同時進行的會議，每個會議都包含數百位參與者且都會使用視訊播放和檔案共用，而這可能會在您的網路上造成大混亂。此外，有時可能也會有法律顧慮。例如，會議參與者預設可以在共用內容上加上註解；不過封存會議時並不會儲存這些註解。如果您的組織需要保留所有電子通訊的記錄，您可能需要停用註解。

當然，需要管理會議設定是一回事，實際管理這些設定又是另一回事。在 Lync Server 中，會議是使用會議原則來管理 (在此軟體的舊版中，這些稱為會議原則)。但如上述，會議原則會判斷可在會議中使用的特性與功能；範圍從會議是否可包含 IP 音訊和視訊，到可出席會議的人數上限都涵蓋在內。會議原則可在全域範圍、網站範圍或個別使用者範圍設定。這可為系統管理員在決定哪些使用者可以使用哪些功能時提供了很大的彈性。

當您建立一個網站原則時，該原則會在建立時自動指派至適當的網站。個別使用者原則則不是如此：個別使用者原則不會在建立時指派給任何人。但是，您必須使用 **Grant-CsConferencingPolicy** Cmdlet 將個別使用者會議原則明確指派給使用者或一組使用者。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Grant-CsConferencingPolicy** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsConferencingPolicy"}

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
<td><p>表示應該要被指派原則之使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\kenmyer)；和 4) 使用者的 Active Directory 顯示名稱 (例如 Ken Myer)。也可以透過使用者的 Active Directory 辨別名稱來參考使用者識別。</p>
<p>請注意，在指定使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回所有顯示名稱是以字串 &quot; Smith&quot; 結束的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指派之原則的「名稱」。簡單來說，PolicyName 是原則 Identity 減去原則範圍 (&quot;tag:&quot;首碼)。例如，Identity 為 tag:Redmond 的原則擁有與 Redmond 相等的 PolicyName；而 Identity 為 tag:RedmondConferencingPolicy 的原則則擁有與 RedmondConferencingPolicy 相等的 PolicyName。</p>
<p>若要取消指派先前指派給使用者的個別使用者原則，請將 PolicyName 參數設為 $Null。</p></td>
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
<td><p>允許在指派新原則時，指定要連線網域控制站的完整網域名稱 (FQDN)。若未指定此參數，則 <strong>Grant-CsConferencingPolicy</strong> Cmdlet 將會連絡第一個可用的網域控制站。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您透過代表已被指派原則之使用者的管線來傳遞使用者物件。根據預設，<strong>Grant-CsConferencingPolicy</strong> Cmdlet 不會透過管線傳遞物件。</p></td>
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

字串值或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Grant-CsConferencingPolicy** Cmdlet 接受管線傳送的字串值輸入，代表使用者帳戶的 Identity。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

根據預設，**Grant-CsConferencingPolicy** Cmdlet 不會傳回物件或值。但是，如果加入 PassThru 參數，則 Cmdlet 會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsConferencingPolicy](get-csconferencingpolicy.md)  
[New-CsConferencingPolicy](new-csconferencingpolicy.md)  
[Remove-CsConferencingPolicy](remove-csconferencingpolicy.md)  
[Set-CsConferencingPolicy](set-csconferencingpolicy.md)

