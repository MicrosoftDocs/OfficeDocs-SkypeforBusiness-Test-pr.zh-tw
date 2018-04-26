---
title: Grant-CsPinPolicy
TOCTitle: Grant-CsPinPolicy
ms:assetid: ce5f610b-117b-46b3-ad06-0e93f5b7a4de
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398871(v=OCS.15)
ms:contentKeyID: 49292353
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsPinPolicy

 

_**上次修改主題的時間：** 2015-03-09_

指派使用者或使用者群組的用戶端個人識別碼 (PIN) 原則。PIN 驗證讓使用者在存取 Lync Server 時只需提供 PIN 而無須提供使用者名稱與密碼。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Grant-CsPinPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將原則 RedmondUsersPinPolicy 指派給使用者 kenmyer@litwareinc.com。

    Grant-CsPinPolicy -Identity "kenmyer@litwareinc.com" -PolicyName RedmondUsersPinPolicy

## 範例 2

範例 2 會取消指派任何先前已指派給使用者 kenmyer@litwareinc.com 的個別使用者 PIN 原則。呼叫 **Grant-CsPinPolicy** Cmdlet 並將原則名稱設為 Null 值 ($Null)，可移除任何已指派給使用者的個別使用者原則。

    Grant-CsPinPolicy -Identity kenmyer@litwareinc.com -PolicyName $Null 

## 範例 3

範例 3 會將原則 RedmondUsersPinPolicy 指派給所有在 Redmond 城市工作的使用者。為達成此目的，**Get-CsUser** Cmdlet 會先擷取所有在 Redmond 工作之使用者的集合；作法是加入 LdapFilter 參數搭配篩選值 "l=Redmond" (在 LDAP 篩選器中，l 是小寫字母的 L，代表使用者的位置)。然後將該使用者集合管線傳送到 **Grant-CsPinPolicy** Cmdlet，以將原則 RedmondUsersPinPolicy 指派給每一位使用者。

    Get-CsUser -LdapFilter "l=Redmond" | Grant-CsPinPolicy -PolicyName RedmondUsersPinPolicy

## 範例 4

範例 4 會將原則 RedmondUsersPinPolicy 指派給所有尚未指派個別使用者 PIN 原則的使用者。為了判斷尚未指派 PIN 原則的使用者，會呼叫 **Get-CsUser** Cmdlet 搭配 Filter 參數；篩選值 {ClientPinPolicy -eq $Null} 只會傳回 ClientPinPolicy 屬性為 Null 的使用者 (亦即，尚未指派個別使用者 PIN 原則)。然後將該使用者集合管線傳送到 **Grant-CsPinPolicy** Cmdlet，以將原則 RedmondUsersPinPolicy 指派給集合中的每一位人員。

    Get-CsUser -Filter {PinPolicy -eq $Null} | Grant-CsPinPolicy -PolicyName RedmondUsersPinPolicy

## 詳細描述

Lync Server 可讓使用者透過電話來連接系統或加入公用交換電話網路 (PSTN) 會議。一般說來，在登入系統或加入會議時，使用者必須輸入使用者名稱和密碼。然而很遺憾地，如果您使用的是沒有英數字元鍵盤的電話，輸入使用者名稱和密碼將會是一大難題。基於上述考量，Lync Server 可讓您將僅由數字組成的 PIN 提供給使用者。當出現提示時，使用者只要輸入 PIN 便能登入系統或加入會議，完全不需要使用者名稱和密碼。

Lync Server 使用 PIN 原則來管理 PIN 驗證屬性。例如，您可以指定 PIN 的長度下限，以及決定是否將允許使用「共同模式」(例如，重複數字) 的 PIN (例如，像是 11223344 的 PIN)。您可以在全域範圍或網站範圍設定 PIN 原則。此外，您也可以在個別使用者範圍設定 PIN 原則，然後再指派給某位使用者或一組指定的使用者。若要指派個別使用者原則，您必須使用 **Grant-CsPinPolicy** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Grant-CsPinPolicy** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsPinPolicy"}

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
<td><p>表示要接受個別使用者 PIN 原則指派之使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。也可以使用使用者的 Active Directory 辨別名稱來指定使用者識別。</p>
<p>此外，使用顯示名稱做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會傳回所有顯示名稱結尾為字串值 &quot; Smith&quot; 的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指派之原則的「名稱」。簡單來說，PolicyName 是原則 Identity 減去原則範圍 (&quot;tag:&quot;首碼)。例如，對於 Identity 為 tag:Redmond 的原則，其 PolicyName 等於 Redmond；對於 Identity 為 tag:RedmondUsersPinPolicy 的原則，其 PolicyName 等於 RedmondUsersPinPolicy。若要取消指派先前已指派給使用者的個別使用者原則，請將 PolicyName 設定為 Null 值 ($Null)。</p></td>
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
<td><p>讓您在指派新原則時，可以指定要連絡之網域控制站的完整網域名稱 (FQDN)。如果未指定此參數，則 <strong>Grant-CsPinPolicy</strong> Cmdlet 將連絡第一個可用的網域控制站。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您透過代表已指派原則的使用者之管線傳遞使用者物件。根據預設，<strong>Grant-CsPinPolicy</strong> Cmdlet 不會經由該管線傳遞物件。</p></td>
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

字串值或 Microsoft.Rtc.Management.UserPinService.PinInfoDetails 物件。**Grant-CsPinPolicy** Cmdlet 接受代表使用者帳戶 Identity 之字串值的管線傳送輸入。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

根據預設，**Grant-CsPinPolicy** Cmdlet 不會傳回值或物件。但是，如果加入 PassThru 參數，Cmdlet 就會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact 的執行個體。

## 請參閱

#### 其他資源

[Get-CsPinPolicy](get-cspinpolicy.md)  
[New-CsPinPolicy](new-cspinpolicy.md)  
[Remove-CsPinPolicy](remove-cspinpolicy.md)  
[Set-CsPinPolicy](set-cspinpolicy.md)

