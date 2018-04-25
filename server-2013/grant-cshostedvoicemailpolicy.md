---
title: Grant-CsHostedVoicemailPolicy
TOCTitle: Grant-CsHostedVoicemailPolicy
ms:assetid: ae69358f-1618-4a08-9ec2-225ded3f301f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412829(v=OCS.15)
ms:contentKeyID: 49291994
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsHostedVoicemailPolicy

 

_**上次修改主題的時間：** 2015-03-09_

在個別使用者範圍指派代管的語音信箱原則 (個別使用者範圍可讓您指派原則給個別使用者或群組)。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Grant-CsHostedVoicemailPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例將 Identity 為 ExRedmond 的主控語音信箱原則指派給顯示名稱為 Ken Myer 的使用者。

    Grant-CsHostedVoicemailPolicy -Identity "Ken Myer" -PolicyName ExRedmond

## 範例 2

此範例將 Identity 為 ExRedmond 的主控語音信箱原則指派給 Finance 組織單位 (OU) 的所有使用者：OU=Finance,OU=NorthAmerica,DC=litwareinc,DC=com。命令的第一部分會呼叫 **Get-CsUser** Cmdlet，以便從指定的 OU 中擷取啟用 Lync Server 或 Office Communications Server 的所有使用者。然後將此使用者集合傳送給 **Grant-CsHostedVoicemailPolicy** Cmdlet，由其指派 ExRedmond 原則給其中的每一個使用者。

    Get-CsUser -OU "ou=Finance,ou=North America,dc=litwareinc,dc=com" | Grant-CsHostedVoicemailPolicy -PolicyName ExRedmond

## 詳細描述

這個 Cmdlet 會將現有的使用者專屬主控語音信箱原則指派給使用者。主控的語音信箱原則指定如何將使用者未接聽的來電轉接至主控的 Exchange 整合通訊 (UM) 服務。

您可以使用下列格式呼叫命令，檢查使用者是否已授與個別使用者主控語音信箱原則：Get-CsUser "\<user name\>" | Select-Object HostedVoicemailPolicy。例如：

Get-CsUser "Ken Myer" | Select-Object HostedVoicemailPolicy

如果指派給使用者的主控語音信箱原則不包含目的地，就無法啟用該使用者的主控語音信箱。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Grant-CsHostedVoicemailPolicy** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsHostedVoicemailPolicy"}

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
<td><p>為其指定主控語音信箱原則之使用者的 Identity (唯一識別碼)。</p>
<p>可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式(例如 litwareinc\kenmyer)；和 4) 使用者的 Active Directory 顯示名稱 (例如 Ken Myer)。</p>
<p>請注意，使用顯示名稱做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回姓氏為 Smith 的所有使用者。</p>
<p>完整資料類型：Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指定給使用者的主控語音信箱原則的名稱 (Identity)。(請注意，這只包括 Identity 的名稱部分。個別使用者主控語音信箱原則識別身分包括一個標記前置詞：PolicyName 不應該包含此首碼)。</p></td>
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
<td><p>傳回命令的結果。根據預設，這個 Cmdlet 不會產生任何輸出。</p></td>
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

字串。接受代表已授與主控語音信箱原則的使用者帳戶之 Identity 的管線傳送字串值。

## 傳回類型

搭配 PassThru 參數使用時，會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADUserOrAppContact 類型的物件。

## 請參閱

#### 其他資源

[New-CsHostedVoicemailPolicy](new-cshostedvoicemailpolicy.md)  
[Remove-CsHostedVoicemailPolicy](remove-cshostedvoicemailpolicy.md)  
[Set-CsHostedVoicemailPolicy](set-cshostedvoicemailpolicy.md)  
[Get-CsHostedVoicemailPolicy](get-cshostedvoicemailpolicy.md)  
[Get-CsUser](get-csuser.md)

