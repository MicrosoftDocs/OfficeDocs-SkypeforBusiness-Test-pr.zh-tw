---
title: Lock-CsClientPin
TOCTitle: Lock-CsClientPin
ms:assetid: 81a9895f-96e3-43c9-9dac-8129358e446a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398650(v=OCS.15)
ms:contentKeyID: 49291492
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lock-CsClientPin

 

_**上次修改主題的時間：** 2015-03-09_

可讓系統管理員防止使用者使用個人識別碼 (PIN) 驗證。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Lock-CsClientPin -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會使用 **Lock-CsClientPin** Cmdlet 鎖定屬於使用者 kenmyer@litwareinc.com 的 PIN。

    Lock-CsClientPin -Identity "kenmyer@litwareinc.com"

## 範例 2

範例 2 會使用 **Lock-CsClientPin** Cmdlet 鎖定所有目前已指派 PIN 之使用者的 PIN。作法是使用 **Get-CsUser** Cmdlet，以傳回所有已啟用 Lync Server 之使用者的集合。然後，此集合會管線傳送到 **Get-CsClientPinInfo** Cmdlet，並與 **Where-Object** Cmdlet 搭配使用，以傳回 IsPinSet 屬性等於 True 之使用者的集合。接著將該篩選後的集合管線傳送到 **Lock-CsClientPin** Cmdlet，以鎖定集合中每位使用者的 PIN。

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.IsPinSet -eq $True} | Lock-CsClientPin

## 範例 3

範例 3 會使用 **Lock-CsClientPin** Cmdlet 鎖定 PIN 已經過期之所有使用者的 PIN。為了執行此工作，會先呼叫 **Get-CsUser** Cmdlet 傳回所有啟用 Lync Server 之使用者的集合。然後，此集合會管線傳送到 **Get-CsClientPinInfo** Cmdlet 並搭配使用 **Where-Object** Cmdlet，以將集合限制在 PIN 已過期的使用者。為了判別哪些使用者的 PIN 已過期，**Where-Object** Cmdlet 會檢查帳戶的 PinExpirationTime 屬性 (表示 PIN 號碼過期的日期) 是否早於目前日期 (目前日期是使用 **Get-Date** Cmdlet 擷取)。如果到期日 (例如 2010 年 9 月 1 日) 早於目前日期 (例如 2010 年 9 月 2 日)，即表示 PIN 已經過期。接著會使用 **Lock-CsClientPin** Cmdlet 鎖定每個過期的 PIN。

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.PinExpirationTime -lt (Get-Date)} | Lock-CsClientPin

## 詳細描述

Lync Server 可讓使用者透過電話連接系統或加入公用交換電話網路 (PSTN) 會議。登入系統或加入會議通常需要使用者輸入使用者名稱或密碼。但是，如果您使用的是沒有英數字元鍵盤的電話，輸入使用者名稱和密碼將會是一大難題。基於上述考量，Lync Server 可讓您將僅由數字組成的 PIN 提供給使用者。當出現提示時，使用者只要輸入 PIN 便能登入系統或加入會議，完全不需要使用者名稱和密碼。

Lync Server 可讓您鎖定使用者的 PIN，做為一種安全防護措施。鎖定 PIN 之後，使用者無法再使用該 PIN 存取系統或加入會議 (但是，使用者仍可使用 Lync 2013 等應用程式，以及提供使用者名稱與密碼來存取系統並加入會議)。鎖定 PIN 之後，還原 PIN (及使用者的存取權限) 的唯一方法就是由系統管理員解除鎖定該 PIN。使用 **Unlock-CsClientPin** Cmdlet 可達成此目的。

**Lock-CsClientPin** Cmdlet 可讓系統管理員暫時停用使用者利用 PIN 驗證來存取系統的能力。系統也可能會鎖定 PIN：如果使用者連續多次登入系統失敗，其 PIN 會自動遭到鎖定，並和先前所述一樣，需要由系統管理員解除鎖定。

請注意，當您安裝 Lync Server 標準版時，預設不會啟用 SQL Server Express 的防火牆例外。這代表您無法從 Windows PowerShell 的遠端執行個體執行 **Lock-CsClientPin** Cmdlet；這是因為您的命令無法周遊防火牆並存取 SQL Server Express 資料庫 (但是，您仍然可以在 Standard Edition Server 本機上執行該 Cmdlet)。您必須手動啟用 SQL Server Express 的防火牆例外，才能在遠端執行 **Lock-CsClientPin** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Lock-CsClientPin** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Lock-CsClientPin"}

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
<td><p>PIN 應被鎖定的使用者帳戶識別。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。您也可以使用使用者的 Active Directory 辨別名稱來參照使用者識別。</p>
<p>此外，使用顯示名稱做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會傳回所有顯示名稱結尾為字串值 &quot; Smith&quot; 的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
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

字串值或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Lock-CsClientPin** Cmdlet 可接受管線傳送的字串值輸入，該字串值是代表使用者帳戶的識別。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

**Lock-CsClientPin** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.UserPinService.PinInfoDetails 物件的一或多個執行個體。

## 請參閱

#### 其他資源

[Get-CsClientPinInfo](get-csclientpininfo.md)  
[Set-CsClientPin](set-csclientpin.md)  
[Unlock-CsClientPin](unlock-csclientpin.md)

