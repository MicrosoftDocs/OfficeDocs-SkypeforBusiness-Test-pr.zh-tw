---
title: Grant-CsVoicePolicy
TOCTitle: Grant-CsVoicePolicy
ms:assetid: c8aa8d0f-6fb4-43f7-82b0-38d4da2d5611
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398828(v=OCS.15)
ms:contentKeyID: 49292284
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsVoicePolicy

 

_**上次修改主題的時間：** 2015-03-09_

指派語音原則給一或多個使用者或群組。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Grant-CsVoicePolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

這個範例將 Identity 為 VoicePolicyRedmond 的語音原則指定給顯示名稱為 Ken Myer 的使用者。

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName VoicePolicyRedmond

## 範例 2

這個範例會將 Identity 為 VoicePolicyRedmond 的語音原則指派給 Finance OU 中的所有使用者：OU=Finance,OU=NorthAmerica,DC=litwareinc,DC=com。命令的第一部分會呼叫 **Get-CsUser** Cmdlet，以便從指定的 OU 擷取啟用 Lync Server 或 Office Communications Server 的所有使用者。然後將此使用者集合傳送到 **Grant-CsVoicePolicy** Cmdlet，它會將原則 VoicePolicyRedmond 指定給其中每一個使用者。

    Get-CsUser -OU "ou=Finance,ou=North America,dc=litwareinc,dc=com" | Grant-CsVoicePolicy -PolicyName VoicePolicyRedmond

## 詳細描述

這個 Cmdlet 會指定現有的個別使用者語音原則給使用者。語音原則可用來管理 Enterprise Voice 相關功能，例如同時響鈴 (每次有人撥打到您的辦公室電話時，能夠讓第二支電話響起) 和來電轉接。使用這個 Cmdlet 可為特定使用者指定啟用及停用這些功能的設定。

您可以使用下列格式呼叫命令，檢查使用者是否已授與個別使用者語音原則：Get-CsUser "\<user name\>" | Select-Object VoicePolicy。例如：

Get-CsUser "Ken Myer" | Select-Object VoicePolicy

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Grant-CsVoicePolicy** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsVoicePolicy"}

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
<td><p>為其指定原則之使用者的 Identity (唯一識別碼)。</p>
<p>可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\kenmyer)；和 4) 使用者的 Active Directory 顯示名稱 (例如 Ken Myer)。</p>
<p>請注意，使用顯示名稱做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回姓氏為 Smith 的所有使用者。</p>
<p>完整資料類型：Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指定給使用者的語音原則名稱 (Identity) (請注意，這只包括 Identity 的名稱部分。個別使用者原則識別身分包括前置詞 tag:，PolicyName 不應該包含此首碼)。</p></td>
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

字串。接受代表已授與語音原則之使用者帳戶 Identity 的管線傳送字串值。

## 傳回類型

搭配 PassThru 參數使用時，會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADUserOrAppContact 類型的物件。

## 請參閱

#### 其他資源

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)  
[Get-CsUser](get-csuser.md)

