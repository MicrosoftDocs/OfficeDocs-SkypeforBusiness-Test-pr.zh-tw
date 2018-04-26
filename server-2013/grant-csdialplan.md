---
title: Grant-CsDialPlan
TOCTitle: Grant-CsDialPlan
ms:assetid: 730ad014-b1e8-4f0a-be78-32b1b5488b78
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398547(v=OCS.15)
ms:contentKeyID: 49291303
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsDialPlan

 

_**上次修改主題的時間：** 2015-03-09_

指派撥號對應用表給一或多個使用者或群組。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Grant-CsDialPlan -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例中，**Grant-CsDialPlan** Cmdlet 用於將 RedmondDialPlan 撥號對應表指派給 Identity (在此範例中為顯示名稱) 為 Ken Myer 的使用者。

    Grant-CsDialPlan -Identity "Ken Myer" -PolicyName RedmondDialPlan

## 範例 2

在範例 2 中，RedmondDialPlan 撥號對應表會指派給辦公室位於 Redmond 的所有使用者。為達成此目的，會呼叫 **Get-CsUser** Cmdlet，以擷取辦公室位於 Redmond 市之所有使用者的集合；作法是使用 LdapFilter 參數搭配 LDAP 查詢 l=Redmond (在 Active Directory 網域服務所使用的 LDAP 查詢語言中，l 表示使用者的位置或城市)。然後，此集合會管線傳送到 **Grant-CsDialPlan** Cmdlet，以將 Redmond 撥號對應表指派給集合中的每位使用者。

    Get-CsUser -LDAPFilter "l=Redmond" | Grant-CsDialPlan -PolicyName RedmondDialPlan

## 詳細描述

這個 Cmdlet 會指定現有的使用者專用撥號對應表給使用者。撥號對應表提供可讓 Enterprise Voice 使用者撥打電話所需的資訊。沒有有效撥號對應表的使用者將無法使用 Enterprise Voice 撥打電話。撥號對應表會決定如何套用正規化規則，以及撥打外線時是否必須撥首碼。

您可以使用下列格式呼叫命令，檢查使用者是否已授與個別使用者撥號對應表：Get-CsUser "\<user name\>" | Select-Object DialPlan。例如：

Get-CsUser "Ken Myer" | Select-Object DialPlan

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Grant-CsDialPlan** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsDialPlan"}

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
<td><p>為其指定撥號對應表之使用者的 Identity (唯一識別碼)。</p>
<p>可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。</p>
<p>請注意，使用顯示名稱做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回姓氏為 Smith 的所有使用者。</p>
<p>完整資料類型：Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指派給使用者的撥號對應表之 Identity 值。(請注意，這只包括 Identity 的名稱部分。個別使用者撥號對應表識別身分包括首碼 tag:，PolicyName 不應該包含此首碼)。</p></td>
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

字串。接受代表使用者帳戶 (已被授與撥號對應表) 識別的管線字串值。

## 傳回類型

搭配 PassThru 參數使用時，會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADUserOrAppContact 類型的物件。

## 請參閱

#### 其他資源

[New-CsDialPlan](new-csdialplan.md)  
[Remove-CsDialPlan](remove-csdialplan.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Test-CsDialPlan](test-csdialplan.md)  
[Get-CsUser](get-csuser.md)

