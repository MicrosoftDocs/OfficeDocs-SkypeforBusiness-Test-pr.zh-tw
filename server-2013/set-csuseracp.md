---
title: Set-CsUserAcp
TOCTitle: Set-CsUserAcp
ms:assetid: f3138d9f-fa3e-4a3c-aa8e-f6dbdda8a834
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413018(v=OCS.15)
ms:contentKeyID: 49292789
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUserAcp

 

_**上次修改主題的時間：** 2015-03-09_

為使用者或使用者群組新增音訊會議提供者，或是修改現有指派給使用者的音訊會議提供者。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsUserAcp -Identity <UserIdParameter> -Domain <String> -Name <String> -ParticipantPasscode <String> -TollNumber <String> [-Confirm [<SwitchParameter>]] [-IsDefault <$true | $false>] [-PassThru <SwitchParameter>] [-TollFreeNumbers <String[]>] [-Url <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，**Set-CsUserAcp** Cmdlet 會用來將新的音訊會議提供者指派給使用者 Ken Myer。為達成此目的，會使用 Identity 參數指定要修改的使用者帳戶。此外還會加入必要參數 TollNumber、ParticipantPassCode、Domain 及 Name，並搭配適當的參數值。

    Set-CsUserAcp -Identity "Ken Myer" -TollNumber "14255551298" -ParticipantPassCode 13761 -Domain "fabrikam.com" -Name "Fabrikam ACP"

## 範例 2

範例 2 所示的命令會將相同的音訊會議提供者指派給所有在財務部門工作的使用者。為達成此目的，命令會先使用 **Get-CsUser** Cmdlet 搭配 LdapFilter (並指定篩選值 "Department=Finance")，以傳回所有在財務部門工作的使用者集合。然後，此集合會管線傳送到 **Set-CsUserAcp** Cmdlet，以為集合中的每位使用者指派相同的音訊會議提供者 (Fabrikam ACP)。

    Get-CsUser -LdapFilter "Department=Finance" | Set-CsUserAcp -TollNumber "14255551298" -ParticipantPassCode 13761 -Domain "fabrikam.com" -Name "Fabrikam ACP"

## 範例 3

範例 3 會將 Fabrikam ACP 音訊會議提供者指派給使用者 Ken Myer。除了指定 TollNumber、ParticipantPassCode、Domain 及 Name 之外，此命令還會包含一組免付費電話號碼。為了指定這兩個值，請包含 TollFreeNumbers 參數，後面加上兩個電話號碼，並使用逗號來分隔電話號碼。

    Set-CsUserAcp -Identity "Ken Myer" -TollNumber "14255551298" -ParticipantPassCode 13761 -Domain "fabrikam.com" -Name "Fabrikam ACP" -TollFreeNumbers "18005551010", "18005551020"

## 詳細描述

音訊會議提供者是提供組織會議服務的第三方公司。總而言之，音訊會議提供者提供處於異地之使用者在未連接至公司網路或網際網路，可參與會議或線上會議之語音部分的方法。音訊會議提供者通常會包括高階服務，例如現場翻譯、記錄及現場個別會議總機服務。

Lync Server 不允許與音訊會議提供者完全整合。**CsUserAcp** Cmdlet 讓系統管理員可設定電話號碼和密碼，以及設定在使用者排程會議時隨時可用於音訊會議提供者整合的其他資訊。但是，因為這些 Cmdlet 並非設計來供 Lync Server 的內部部署版本使用 (他們僅供和 Lync Online 搭配使用)，所以，除了指派屬性值之外，不會提供任何其他音訊會議提供者整合。

音訊會議提供者可以使用 **Set-CsUserAcp** Cmdlet 來指派給使用者帳戶。(請注意，使用者可以指派多位音訊會議提供者)。**Set-CsUserAcp** Cmdlet 也可以用來修改現有音訊會議提供者的屬性。如果呼叫 **Set-CsUserAcp** Cmdlet，該 Cmdlet 會使用呼叫所含的參數資訊，來檢查已指派給使用者的現有音訊會議提供者。如果找到相符項，則會修改現有的提供者。例如，假設您發出下列命令：

Set-CsUserAcp –Identity "Ken Myer" –TollNumber "15554251298" –ParticipantPassCode 13761 –Domain "fabrikam.com" –Name "Fabrikam ACP"

然後假設 Ken Myer 已經指派了名為 Fabrikam ACP 的音訊會議提供者，此提供者擁有與命令內所指定之提供者相同的 TollNumber 和 Domain。(換句話說，唯一的不同是 ParticipantPassCode)。在此案例中，**Set-CsUserAcp** Cmdlet 將修改現有的 Fabrikam ACP 提供者。如果找不到相符項，則會將新的提供者新增至 Ken Myer 的使用者帳戶。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsUserAcp** Cmdlet：RTCUniversalUserAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUserAcp"}

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
<td><p><em>Domain</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>音訊會議提供者的網域名稱。例如：-Domain &quot;fabrikam.com&quot;。</p>
<p>網域名稱將由音訊會議提供者提供。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>表示要修改之使用者帳戶的 Identity。您可以使用下列四種格式的其中一種來指定使用者的 Identity：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\kenmyer)；4) 使用者的 Active Directory 網域服務 顯示名稱 (如 Ken Myer)。也可以透過使用者的 Active Directory 辨別名稱來參考使用者識別。</p>
<p>使用「顯示名稱」做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回所有顯示名稱是以字串 &quot;Smith&quot; 結束的使用者。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>音訊會議提供者的名稱。例如：-Name &quot;Fabrikam Conference Services&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>ParticipantPasscode</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>使用音訊會議提供者連接至會議時所需的密碼。例如：-PassCode &quot;0712&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>TollNumber</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>用於音訊會議的非免付費電話號碼。例如：-TollNumber &quot;14255551298&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>IsDefault</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出這是否為使用者的預設音訊會議提供者。每位使用者只能有一位預設提供者。</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您透過管線傳遞代表要設定帳戶屬性之使用者的物件。在這種情況下，PassThru 參數為必要，因為根據預設，<strong>Set-CsUserAcp</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>TollFreeNumbers</em></p></td>
<td><p>選用</p></td>
<td><p>System.String[]</p></td>
<td><p>適用於音訊會議的免付費電話號碼集合。例如：-TollFreeNumbers &quot;18005551298&quot;。若要新增多個免付費號碼，請使用逗號來分隔個別號碼：-TollFreeNumber &quot;18005551298&quot;, &quot;18005559876&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Url</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>音訊會議提供者的 Web URL，例如：-Url &quot;http://acp.fabrikam.com&quot;。Web URL 可以讓音訊會議提供者將使用者指向包含其他撥入電話號碼的網頁，以及音訊會議提供者提供的服務相關資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Set-CsUserAcp** Cmdlet 會接受代表使用者帳戶 (已為 Lync Server 啟用) 之 Identity 的管線字串值。此 Cmdlet 也接受管線傳送的 Active Directory 使用者物件執行個體。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Get-CsUserAcp](get-csuseracp.md)  
[Remove-CsUserAcp](remove-csuseracp.md)

