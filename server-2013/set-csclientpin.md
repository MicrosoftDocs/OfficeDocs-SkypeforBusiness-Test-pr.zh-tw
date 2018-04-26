---
title: Set-CsClientPin
TOCTitle: Set-CsClientPin
ms:assetid: d587c69c-9cf7-4cd8-81d4-26869524654b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398929(v=OCS.15)
ms:contentKeyID: 49292459
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClientPin

 

_**上次修改主題的時間：** 2015-03-09_

指派新的個人識別碼 (PIN) 給指定的使用者。Lync Server 2010 中已導入此 Cmdlet。請注意，此 Cmdlet 的 Lync Server 2013 版本只可指派 PIN 碼給位於 Lync Server 2013 上的使用者。若要指派 PIN 碼給位於 Lync Server 2010 上的使用者，必須使用 Set-CsClientPin 的 Lync Server 2010 版本。

## 語法

    Set-CsClientPin -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Pin <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會為使用者 litwareinc\\kenmyer 指派新自動產生的 PIN。若要指派自動產生的 PIN，請在呼叫 **Set-CsClientPin** Cmdlet 時略過 Pin 參數。當命令完成後，指派給 Ken Myer 的新 PIN 將會顯示於螢幕上，而系統也會將該資訊轉送給使用者。

    Set-CsClientPin -Identity "litwareinc\kenmyer"

## 範例 2

範例 2 中的命令可將 PIN 18723834 指派給使用者 litwareinc\\kenmyer。您可以使用 Pin 參數後面加上要指派的號碼來指派特定的 PIN。

    Set-CsClientPin -Identity "litwareinc\kenmyer" -Pin 18723834

## 範例 3

範例 3 示範如何將新的 PIN 自動指派給指定 Active Directory 組織單位 (OU) 中的所有使用者。為達成此目的，會使用 **Get-CsUser** Cmdlet 搭配 OU 參數，以傳回所有在 Finance OU 中擁有帳戶的使用者集合。然後將該集合管線傳到 **Set-CsClientPin** Cmdlet，以為集合中的每一位使用者產生新的 PIN。

    Get-CsUser -OU "OU=Finance,DC=litwareinc,DC=com" | Set-CsClientPin

## 範例 4

範例 4 所示的命令可將新的 PIN 指派給所有目前尚未有 PIN 指派的使用者。為了完成此工作，會使用 **Get-CsUser** Cmdlet，以傳回所有已針對 Lync Server 啟用的使用者集合。接著將該集合管線傳送到 **Get-CsClientPin** Cmdlet 和 **Where-Object** Cmdlet；使用這兩個 Cmdlet，只選取 IsPinSet 屬性等於 False 的使用者。產生的集合只會包含沒有 PIN 的使用者，接著將集合管線傳送到 **Set-CsClientPin** Cmdlet，以為集合中的每一位使用者自動產生 PIN。

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.IsPinSet -eq $False} | Set-CsClientPin

## 詳細描述

Lync Server 可讓使用者透過電話來連接系統或加入公用交換電話網路 (PSTN) 會議。登入系統或加入會議通常需要使用者輸入使用者名稱或密碼。但是，如果您使用的是沒有英數字元鍵盤的電話，輸入使用者名稱和密碼將會是一大難題。基於上述考量，Lync Server 可讓您將僅由數字組成的 PIN 提供給使用者。當出現提示時，使用者只要輸入 PIN 便能登入系統或加入會議，完全不需要使用者名稱和密碼。

當使用者已啟用 Lync Server 時，系統並不會指派 PIN 給使用者。也就是說，根據預設，使用者不能使用 PIN 驗證存取系統。使用者可從電話撥入式會議網頁取得 PIN；或者，系統管理員可以使用 **Set-CsClientPin** Cmdlet，將 PIN 指派給每位使用者。您可以利用 **Set-CsClientPin** Cmdlet，將特定的 PIN 指派給使用者，或允許 Lync Server 為您產生 PIN。若要自動產生 PIN，只要在呼叫 **Set-CsClientPin** Cmdlet 時省略 PIN 參數即可。執行上述作業後，就會產生新的 PIN，當命令完成時，使用者 Identity 和其新的 PIN 將顯示於螢幕上。

請注意，您明確指派的 PIN 必須要和負責控管有問題之使用者的 PIN 驗證原則中的指定條件相符。例如，PIN 的位數至少必須和 MinPasswordLength 屬性指定的位數相等。另請注意，PIN 只能含有數字，不允許使用字母或其他非數字的字元。

當您使用 **Set-CsClientPin** Cmdlet 來設定用戶端 PIN 時，不會強制執行 PIN 碼歷程記錄計數。例如，假設使用者的 PIN 號碼是 12345，而其用戶端 PIN 原則會防止他們立即重複使用相同的 PIN 號碼。如果該使用者嘗試使用電話撥入式會議網頁來更新其用戶端 PIN，則任何嘗試重複使用相同 PIN 號碼 (12345) 的作業都將遭到拒絕。但是，透過使用 **Set-CsClientPin** Cmdlet，系統管理員可以將 PIN 12345 發給該使用者。這是因為 **Set-CsClientPin** Cmdlet 並未受到 PIN 原則歷程記錄計數所束縛。

請注意，當您安裝 Lync Server 標準版時，預設不會啟用 SQL Server Express 的防火牆例外。這代表您無法從 Windows PowerShell 的遠端執行個體執行 **Set-CsClientPin** Cmdlet；這是因為您的命令無法周遊防火牆並存取 SQL Server Express 資料庫 (但是，您仍然可以在 Standard Edition Server 本機上執行 Cmdlet)。您必須手動啟用 SQL Server Express 的防火牆例外，才能針對 Standard Edition Server 在遠端執行 **Set-CsClientPin** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsClientPin** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClientPin"}

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
<td><p>應為其設定 PIN 之使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。也可以透過使用者的 Active Directory 辨別名稱來參考使用者識別。</p>
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
<td><p><em>Pin</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要指派給使用者的選用 PIN。若未加入 PIN 參數，Lync Server 便會隨機產生 PIN 並指派給有問題的使用者。請注意，PIN 必須和指派給使用者之用戶端 PIN 原則中的長度下限及共同模式等設定相符。</p></td>
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

字串值或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Set-CsClientPin** Cmdlet 接受代表使用者帳戶 Identity 之字串值的管線傳送輸入。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

**Set-CsClientPin** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.UserPinService.PinInfoDetails 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsClientPinInfo](get-csclientpininfo.md)  
[Lock-CsClientPin](lock-csclientpin.md)  
[Unlock-CsClientPin](unlock-csclientpin.md)

