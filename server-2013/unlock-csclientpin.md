---
title: Unlock-CsClientPin
TOCTitle: Unlock-CsClientPin
ms:assetid: eef7877c-0302-4ce7-84f5-06968d0623b9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412982(v=OCS.15)
ms:contentKeyID: 49292732
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Unlock-CsClientPin

 

_**上次修改主題的時間：** 2015-03-09_

可讓系統管理員解除鎖定指定使用者的個人識別碼 (PIN)。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Unlock-CsClientPin -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，使用 **Unlock-CsClientPin** Cmdlet 來解除鎖定隸屬於使用者 litwareinc\\kenmyer 的 PIN。

    Unlock-CsClientPin -Identity "litwareinc\kenmyer"

## 範例 2

在範例 2 中，會使用 **Unlock-CsClientPin** Cmdlet 解除鎖定目前已鎖定的所有 PIN。為達成此目的，會先使用 **Get-CsUser** Cmdlet 傳回已啟用 Lync Server 之所有使用者的集合。然後，此集合會管線傳送到 **Get-CsClientPinInfo** Cmdlet，並與 **Where-Object** Cmdlet 搭配使用，以選取 IsLockedOut 屬性等於 (-eq) True ($True) 的使用者。

接著，產生的篩選集合接著會管線傳送到 **Unlock-CsClientPin** Cmdlet，該 Cmdlet 會針對先前已鎖定 PIN 的每位使用者，解除鎖定 PIN。

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.IsLockedOut -eq $True} | Unlock-CsClientPin 

## 詳細描述

Lync Server 可讓使用者透過電話連接系統或加入公用交換電話網路 (PSTN) 會議。登入系統或加入會議通常需要使用者輸入使用者名稱或密碼。但是，如果您使用的是沒有英數字元鍵盤的電話，輸入使用者名稱和密碼將會是一大難題。基於上述考量，Lync Server 可讓您將僅由數字組成的 PIN 提供給使用者。當出現提示時，使用者只要輸入 PIN 便能登入系統或加入會議，完全不需要使用者名稱和密碼。

但是，唯有當使用者的 PIN 已解除鎖定時，此條件才會成立。如果 PIN 號碼已遭鎖定 (可能是因為使用者重複登入失敗，或者因為系統管理員明確鎖定該 PIN)，該使用者將無法使用 PIN 驗證來存取系統或加入會議 (但該使用者仍能透過提供使用者名稱和密碼的方式，使用諸如 Lync 的應用程式來登入系統)。如果某個 PIN 已遭鎖定，則只有一個方法可以還原使用者使用 PIN 驗證來存取系統的能力：必須由系統管理員解除鎖定該鎖定的 PIN。使用 **Unlock-CsClientPin** Cmdlet 可達成此目的。

請注意，當您安裝 Lync Server 標準版時，預設不會啟用 SQL Server Express 的防火牆例外。這表示您無法從 Windows PowerShell 的遠端執行個體執行 **Unlock-CsClientPin** Cmdlet；這是因為您的命令無法周遊防火牆並存取 SQL Server Express 資料庫 (但是，您仍然可以在 Standard Edition Server 本機上執行 Cmdlet)。您必須手動啟用 SQL Server Express 的防火牆例外，才能針對 Standard Edition Server 在遠端執行 **Unlock-CsClientPin** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Unlock-CsClientPin** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Unlock-CsClientPin"}

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
<td><p>PIN 應被解除鎖定的使用者帳戶之 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。也可以透過使用者的 Active Directory 辨別名稱來參考使用者識別。</p>
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
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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

字串值或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Unlock-CsClientPin** Cmdlet 會接受代表使用者帳戶識別之字串值的管線傳送資料。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

**Unlock-CsClientPin** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.UserPinService.PinInfoDetails 物件的一或多個執行個體。

## 請參閱

#### 其他資源

[Get-CsClientPinInfo](get-csclientpininfo.md)  
[Lock-CsClientPin](lock-csclientpin.md)  
[Set-CsClientPin](set-csclientpin.md)

