---
title: Grant-CsArchivingPolicy
TOCTitle: Grant-CsArchivingPolicy
ms:assetid: 675f5d8d-d8f9-4d19-b11b-75df48b09467
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398475(v=OCS.15)
ms:contentKeyID: 49291164
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsArchivingPolicy

 

_**上次修改主題的時間：** 2015-03-09_

可讓您為使用者或使用者群組指派立即訊息 (IM) 工作階段封存原則。這些原則可讓您封存內部使用者之間及/或封存內部使用者與外部協力廠商之間所發生的所有 IM 工作階段。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Grant-CsArchivingPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 中，封存原則 RedmondArchivingPolicy 會指派給顯示名稱為 "Ken Myer" 的使用者。請注意，在 **Grant-CsArchivingPolicy** Cmdlet 中，Identity 屬性指的是使用者的 Identity，而不是封存原則的 Identity，並使用 PolicyName 參數來指定要指派的原則；參數值是原則的 Identity (不包含 "tag:" 前置詞)。

    Grant-CsArchivingPolicy -Identity "Ken Myer" -PolicyName RedmondArchivingPolicy

## 範例 2

範例 2 會將封存原則 RedmondArchivingPolicy 指派給 Redmond 組織單位 (OU) 內擁有帳戶的所有使用者。為達成此目的，命令會使用 **Get-CsUser** Cmdlet 和 OU 參數，以傳回 OU (辨別名稱為 "OU=Redmond,dc=litwareinc,dc=com") 內擁有帳戶之所有使用者的集合。接著會將此集合管線傳送到 **Grant-CsArchivingPolicy** Cmdlet，這會將 RedmondArchivingPolicy 指派給集合中的每位使用者。

    Get-CsUser -OU "OU=Redmond,dc=litwareinc,dc=com" | Grant-CsArchivingPolicy -PolicyName RedmondArchivingPolicy

## 範例 3

範例 3 所示的命令會將 RedmondArchivingPolicy 原則指派給在 Redmond 工作的每位使用者。為了執行此工作，會呼叫 **Get-CsUser** Cmdlet 並搭配 LdapFilter 參數；LDAP 篩選值 "l=Redmond" 可傳回在 Redmond 市工作之所有使用者的集合。(在 LDAP 查詢語言中，l (L 的小寫) 代表「地區」(城市) 的簡稱。) 然後，再將該集合管線傳送到 **Grant-CsArchivingPolicy** Cmdlet，以將 RedmondArchivingPolicy 原則指派給集合中的每位使用者。

    Get-CsUser -LdapFilter "l=Redmond" | Grant-CsArchivingPolicy -PolicyName RedmondArchivingPolicy

## 範例 4

範例 4 會將 RedmondArchivingPolicy 原則指派給位於 atl-cs-001.litwareinc.com 登錄器集區的所有使用者。為達成此目的，會先使用 **Get-CsUser** Cmdlet 傳回所有啟用 Lync Server 的使用者。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 RegistrarPool 等於 atl-cs-001-litwareinc.com 的使用者。接著將篩選後的集合管線傳送到 **Grant-CsArchivingPolicy** Cmdlet，以將 RedmondArchivingPolicy 原則指派給集合中的每位使用者。

    Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Grant-CsArchivingPolicy -PolicyName RedmondArchivingPolicy

## 範例 5

範例 5 會尋找已指派 RedmondArchivingPolicy 原則的所有使用者，然後指派每位使用者不同的原則：NorthAmericaArchivingPolicy。為了執行此工作，會使用 **Get-CsUser** Cmdlet，以傳回啟用 Lync Server 之所有使用者的集合；Filter 參數與篩選值 {ArchivingPolicy -eq "RedmondArchivingPolicy"} 可限制傳回的資料是 ArchivingPolicy 等於 "RedmondArchivingPolicy" 的帳戶。然後再將篩選後的集合管線傳送到 **Grant-CsArchivingPolicy** Cmdlet，以將 NorthAmericaArchivingPolicy 原則指派給集合中的每位使用者。

    Get-CsUser -Filter {ArchivingPolicy -eq "RedmondArchivingPolicy"} | Grant-CsArchivingPolicy -PolicyName "NorthAmericaArchivingPolicy"

## 範例 6

範例 6 是範例 5 的變化。但是，這次是對先前已指派 RedmondArchivingPolicy 原則的使用者進行解除指派：呼叫 **Grant-CsArchivingPolicy** Cmdlet 並搭配 PolicyName 等於 $Null，這樣會移除先前指派的個別使用者原則。

    Get-CsUser -Filter {ArchivingPolicy -eq "RedmondArchivingPolicy"} | Grant-CsArchivingPolicy -PolicyName $Null

## 詳細描述

許多組織都發現保留其使用者參與之所有 IM 工作階段的封存很有用處；有些組織則是依法保留此類封存。您必須執行兩項步驟，才能使用 Lync Server 封存 IM 工作階段。首先，您需要使用 **Set-CsArchivingConfiguration** Cmdlet，在全域範圍和/或網站範圍啟用封存。這可讓您能夠封存 IM 工作階段，不過，它不會自動開始封存這些工作階段。

若要真的儲存 IM 工作階段記錄，您必須完成步驟 2：建立一個或多個 IM 工作階段封存原則。這些原則決定哪些使用者可記錄 IM 工作階段，以及要封存哪些類型的 IM 工作階段 (內部和/或外部)。內部 IM 工作階段是指，其中的所有參與者都是經過驗證的使用者，他們在組織內擁有 Active Directory 帳戶。相較之下，外部 IM 工作階段是指，其中至少有一位參與者是未驗證的使用者，他們在組織內沒有 Active Directory 帳戶。您可以選擇只封存內部工作階段、只封存外部工作階段，或內部和外部工作階段都封存。

封存原則可以指派給全域範圍或網站範圍。此外，這些原則還可以指派給個別使用者範圍，然後套用至特定使用者或特定一組使用者。例如，假設您的全域原則只封存內部 IM 工作階段。在此情況下，您可以建立同時封存內部和外部工作階段的次要原則，然後只將該原則套用到您自己的銷售人員。因為個別使用者原則優先於全域和網站原則，所以銷售人員的成員可以封存全部的 IM 工作階段。其他使用者 (也就是不在銷售部門且不受銷售原則影響的使用者) 就只會封存其內部 IM 工作階段。

**Grant-CsArchivingPolicy** Cmdlet 可用來指派個別使用者封存原則至使用者或指定的使用者集。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Grant-CsArchivingPolicy** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsArchivingPolicy"}

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
<td><p>指出要將原則指派給哪一個使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\kenmyer)；和 4) 使用者的 Active Directory 顯示名稱 (例如 Ken Myer)。也可以透過使用者的 Active Directory 辨別名稱來參考使用者識別。</p>
<p>此外，使用顯示名稱做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回所有顯示名稱是以字串值 &quot; Smith&quot; 結束的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指派之原則的「名稱」。PolicyName 只是原則 Identity 減去範圍指示項 &quot;tag:&quot;。例如，含有 Identity 為 tag:Redmond 之原則的 PolicyName 等於 Redmond；含有 Identity 為 tag:RedmondArchivingPolicy 之原則的 PolicyName 等於 RedmondArchivingPolicy。</p>
<p>若要移除已指派給使用者的個別使用者原則，請將 PolicyName 設為 Null 值：</p>
<p>-PolicyName $Null</p></td>
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
<td><p>可讓您指定指派原則時連線的網域控制站。如果未包含此參數，Cmdlet 會使用第一個可用的網域控制站。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，會使得 Cmdlet 透過 Windows PowerShell 管線傳遞一或多個使用者物件。根據預設，<strong>Grant-CsArchivingPolicy</strong> Cmdlet 不會透過管線傳遞物件。</p></td>
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

字串值或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Grant-CsArchivingPolicy** Cmdlet 可接受管線傳送的字串值輸入，該字串值是代表使用者帳戶的識別。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

**Grant-CsArchivingPolicy** Cmdlet 不會傳回值或物件，而會將 Microsoft.Rtc.Management.WritableConfig.Policy.IM.ImArchivingPolicy 物件的執行個體指派給使用者或使用者群組。但是，如果加入 PassThru 參數，Cmdlet 就會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact 的執行個體。

## 請參閱

#### 其他資源

[Get-CsArchivingPolicy](get-csarchivingpolicy.md)  
[New-CsArchivingPolicy](new-csarchivingpolicy.md)  
[Remove-CsArchivingPolicy](remove-csarchivingpolicy.md)  
[Set-CsArchivingPolicy](set-csarchivingpolicy.md)

