---
title: Get-CsClientPinInfo
TOCTitle: Get-CsClientPinInfo
ms:assetid: 45feaa2c-f284-4374-a8a6-d3ff3c87d660
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425947(v=OCS.15)
ms:contentKeyID: 49290780
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClientPinInfo

 

_**上次修改主題的時間：** 2015-03-09_

擷取指派給使用者的個人識別碼 (PIN) 相關資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsClientPinInfo -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會傳回已啟用 Lync Server 之所有使用者的 PIN 資訊。為達成此目的，命令會先呼叫 **Get-CsUser** Cmdlet 傳回所有啟用 Lync Server 的使用者。然後再將該集合傳送到 **Get-CsClientPinInfo** Cmdlet，以顯示集合中每位使用者的 PIN 資訊。

    Get-CsUser | Get-CsClientPinInfo

## 範例 2

在範例 2 中，**Get-CsClientPinInfo** Cmdlet 用來顯示單一使用者的 PIN 資訊：Identity 為 litwareinc\\kenmyer 的使用者。

    Get-CsClientPinInfo -Identity "litwareinc\kenmyer"

## 範例 3

範例 3 會傳回在 Finance 組織單位 (OU) 中具有帳戶之所有使用者的 PIN 資訊。為達成此目的，會使用 **Get-CsUser** Cmdlet 和 OU 參數傳回 Finance OU 中所有使用者的集合。接著，該集合會管線傳送到 **Get-CsClientPinInfo** Cmdlet，以顯示集合中每個使用者的 PIN 資訊。

    Get-CsUser -OU "OU=Finance,DC=litwareinc,DC=com" | Get-CsClientPinInfo

## 範例 4

範例 4 所示的命令會顯示組織中所有 Manager 的 PIN 資訊。若要擷取所有 Manager 的集合，此命令會使用 **Get-CsUser** Cmdlet 搭配 LDAPFilter 參數；篩選值 "Title=Manager" 會將傳回的集合限制為其職稱為 "Manager" 的使用者。接著，使用 **Get-CsClientPinInfo** Cmdlet 顯示這些使用者每一個的 PIN 資訊。

    Get-CsUser -LdapFilter "Title=Manager" | Get-CsClientPinInfo

## 詳細描述

Lync Server 可讓使用者透過電話連接系統或加入公用交換電話網路 (PSTN) 會議。登入系統或加入會議通常需要使用者輸入使用者名稱或密碼。但是，如果您使用沒有英數鍵盤的電話，則輸入使用者名稱及密碼會是個問題。基於上述考量，Lync Server 可讓您將僅由數字組成的 PIN 提供給使用者。當出現提示時，使用者只要輸入 PIN 便能登入系統或加入會議，完全不需要使用者名稱和密碼。

系統管理員可以執行 **Get-CsClientPinInfo** Cmdlet 來擷取使用者或使用者群組的 PIN 設定。請注意，系統管理員無法擷取已指派給使用者的 PIN。如果使用者忘記其 PIN，將無法使用 PIN 驗證來存取系統，要等到系統管理員指派新的 PIN 之後，或者等到使用者從 \[電話撥入式會議\] 網頁取得新的 PIN 之後才可以。

請注意，當您安裝 Lync Server 標準版時，預設不會啟用 SQL Server Express 的防火牆例外。這表示您無法從 Windows PowerShell 的遠端執行個體執行 **Get-CsClientPinInfo** Cmdlet，因為您的命令無法周遊防火牆並存取 SQL Server Express 資料庫 (但是，您仍可以在 Standard Edition 伺服器上本機執行此 Cmdlet)。若要針對 Standard Edition 伺服器遠端執行 **Get-CsClientPinInfo** Cmdlet，您必須手動針對 SQL Server Express 啟用防火牆例外狀況。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsClientPinInfo** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClientPinInfo"}

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
<td><p>表示應鎖定其 PIN 之使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。您也可以利用使用者的 Active Directory 辨別名稱來參考使用者帳戶。</p>
<p>使用「顯示名稱」做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回顯示名稱結尾為字串值 &quot; Smith&quot; 的所有使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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

字串值或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Get-CsClientPinInfo** Cmdlet 接受管線傳送的字串值輸入，代表使用者帳戶的 Identity。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

**Get-CsClientPinInfo** Cmdlet 會傳回 Microsoft.Rtc.Management.UserPinService.PinInfoDetails 物件的一或多個執行個體。

## 請參閱

#### 其他資源

[Get-CsPinPolicy](get-cspinpolicy.md)  
[Lock-CsClientPin](lock-csclientpin.md)  
[Set-CsClientPin](set-csclientpin.md)  
[Unlock-CsClientPin](unlock-csclientpin.md)

