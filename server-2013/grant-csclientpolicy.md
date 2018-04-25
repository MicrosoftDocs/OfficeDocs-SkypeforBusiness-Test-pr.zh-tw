---
title: Grant-CsClientPolicy
TOCTitle: Grant-CsClientPolicy
ms:assetid: c09d743d-cf2c-4622-b00c-cc815852e4a6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412942(v=OCS.15)
ms:contentKeyID: 49292194
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsClientPolicy

 

_**上次修改主題的時間：** 2015-03-09_

指派用戶端原則給使用者或使用者群組。用戶端原則可指定使用者所能使用的 Lync Server 功能。例如，您可能會在授權某些使用者可以傳輸檔案的同時，也拒絕讓某些使用者執行此作業。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Grant-CsClientPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，用戶端原則 SalesPolicy 會指派給 Identity 為 Ken Myer 的使用者。

    Grant-CsClientPolicy -Identity "Ken Myer" -PolicyName SalesPolicy

## 範例 2

範例 2 會將 SalesPolicy 用戶端原則指派給 Sales 部門的所有使用者。命令會先使用 **Get-CsUser** Cmdlet 搭配 LdapFilter 參數，以傳回 Sales 部門成員的所有使用者集合。然後將此使用者集合管線傳送到 **Grant-CsClientPolicy** Cmdlet，以將 SalesPolicy 原則指派給集合中的每一位使用者。

    Get-CsUser -LDAPFilter "Department=Sales" | Grant-CsClientPolicy -PolicyName SalesPolicy

## 範例 3

範例 3 會將 RedmondAccountingPolicy 用戶端原則指派給所有符合下列兩項準則的使用者：1) 使用者必須有工作職稱 Accountant；且 2) 使用者必須在 Redmond 城市工作。為達成此目的，命令會先使用 **Get-CsUser** Cmdlet 搭配 LdapFilter 參數，以傳回在 Redmond 工作且工作職稱為 Accountant 的所有使用者集合。篩選值 "(&(Title=Accountant)(l=Redmond))" 會將傳回的資料限制在工作職稱為 Accountant (Title=Accountant) 且 (&) 在 Redmond 工作 (l=Redmond) 的使用者 ("l" 是小寫字母的 L，表示使用者的位置)。

然後將產生的集合管線傳送到 **Grant-CsClientPolicy** Cmdlet，以將 RedmondAccountingPolicy 原則指派給集合中的每一位使用者。

    Get-CsUser -LDAPFilter "(&(Title=Accountant)(l=Redmond))" | Grant-CsClientPolicy -PolicyName RedmondAccountingPolicy

## 範例 4

範例 4 會將 AccountingPolicy 原則指派給所有符合下列兩項準則之一的使用者：使用者的工作職稱為 Accountant 或使用者的工作職稱為 Senior Accountant。為了執行此工作，會使用 **Get-CsUser** Cmdlet 搭配 LdapFilter 參數，以傳回工作職稱為 Accountant 或 Senior Accountant 的使用者集合 (篩選值 "(|(Title=Accountant)(Title=Senior Accountant))" 可將傳回的資料限制在工作職稱為 Accountant (Title=Accountant) 或 (|) Senior Accountant (Title=Senior Accountant) 的使用者)。然後將此篩選後的集合管線傳送到 **Grant-CsClientPolicy** Cmdlet，以將 AccountingPolicy 用戶端原則指派給集合中的每一位使用者。

    Get-CsUser -LdapFilter "(|(Title=Accountant)(Title=Senior Accountant))" | Grant-CsClientPolicy -PolicyName AccountingPolicy

## 範例 5

範例 5 會將 AtlantaBranchPolicy 用戶端原則指派給帳戶屬於登錄器集區 atl-cs-001.litwareinc.com 的所有使用者。為達成此目的，會先呼叫 **Get-CsUser** Cmdlet，以傳回適當的使用者帳戶；Filter 參數和篩選值 {RegistrarPool -eq "atl-cs-001.litwareinc.com"} 確保只會傳回帳戶屬於登錄器集區 atl-cs-001.litwareinc.com 的使用者。然後，此集合會管線傳送到 **Grant-CsClientPolicy** Cmdlet，以將 AtlantaBranchPolicy 用戶端原則指派給每一位使用者。

    Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Grant-CsClientPolicy -PolicyName AtlantaBranchPolicy

## 詳細描述

在 Lync Server 中，用戶端原則取代了舊版產品中所使用的「群組原則」設定。在 Microsoft Office Communicator 2007 和 Microsoft Office Communicator 2007 R2 中，可使用「群組原則」協助決定使用者可以用 Communicator 做些什麼；例如，「群組原則」設定決定使用者是否可以儲存其立即訊息交談的記錄、來自 Microsoft Outlook 的資訊是否整合到他們的目前狀態資訊，以及使用者是否可以在立即訊息中加入表情或格式化文字。

儘管「群組原則」如此有用，它在技術上仍有限制，尤其是在套用到 Lync Server 時。首先，「群組原則」的設計是根據個別網域或個別組織單位 (OU) 而套用原則；這使得它很難將原則套用到更精確選取的使用者群組 (例如，在特定部門工作的所有使用者，或是所有有特定工作職稱的使用者)。另一方面，\[群組原則\] 只會套用到登入網域的使用者，以及使用電腦登入的使用者；\[群組原則\] 不會套用到透過網際網路存取 Lync Server 的使用者，或使用行動電話存取系統的使用者。這就表示，同一名使用者隨著登入裝置以及登入位置的不同，就會有不同的使用經驗。

為了解決這些不一致的問題，Lync Server 會使用用戶端原則而不是「群組原則」。用戶端原則會在使用者每一次存取系統時套用，不管使用者從何處登入以及使用何種裝置登入。此外，用戶端原則 (如同其他 Lync Server 原則) 很容易便可套用到選取的使用者群組。您甚至可以建立指派給單一使用者的自訂原則。

用戶端原則可在全域、網站和個別使用者範圍設定。若要指派個別使用者原則給使用者，必須使用 **Grant-CsClientPolicy** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Grant-CsClientPolicy** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsClientPolicy"}

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
<td><p>指出要將原則指派給哪一個使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。也可以透過使用者的 Active Directory 辨別名稱來參考使用者識別。</p>
<p>此外，使用顯示名稱做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回所有顯示名稱是以字串值 &quot; Smith&quot; 結束的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指派之原則的「名稱」。簡單來說，PolicyName 是原則 Identity 減去原則範圍 (&quot;tag:&quot;)。例如，Identity 為 tag:Redmond 的原則擁有與 Redmond 相等的 PolicyName；而 Identity 為 tag:RedmondConferencingPolicy 的原則則擁有與 RedmondConferencingPolicy 相等的 PolicyName。</p>
<p>如果將 PolicyName 設為 Null 值，這個命令會將指派給該名使用者的所有個別使用者原則皆取消指派。例如：</p>
<p>Grant-CsClientPolicy –Identity &quot;Ken Myer&quot; –PolicyName $Null</p></td>
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
<td><p>可讓您指定指派原則時連線的網域控制站。若未加入此參數，Cmdlet 會使用第一個可用的網域控制站。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，會使得 Cmdlet 透過 Windows PowerShell 管線傳遞一或多個使用者物件。根據預設，<strong>Grant-CsClientPolicy</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
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

字串值或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Grant-CsClientPolicy** Cmdlet 接受代表使用者帳戶 Identity 之字串值的管線傳送輸入。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

根據預設，**Grant-CsClientPolicy** Cmdlet 不會傳回物件或值。但是，如果加入 PassThru 參數，則 Cmdlet 會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsClientPolicy](get-csclientpolicy.md)  
[New-CsClientPolicy](new-csclientpolicy.md)  
[Remove-CsClientPolicy](remove-csclientpolicy.md)  
[Set-CsClientPolicy](set-csclientpolicy.md)

