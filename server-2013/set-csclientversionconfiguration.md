---
title: Set-CsClientVersionConfiguration
TOCTitle: Set-CsClientVersionConfiguration
ms:assetid: 7cd2e86f-2d31-4db2-9d0f-f1418fd4aba2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398623(v=OCS.15)
ms:contentKeyID: 49291436
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClientVersionConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改指定的用戶端版本組態設定集合。用戶端版本組態設定可指定 Lync Server 是否需要檢查登入系統之所有用戶端應用程式的版本號碼。如有啟用用戶端版本篩選，則用戶端應用程式存取系統的能力，將視相關用戶端版本原則中所設定的設定而定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsClientVersionConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClientVersionConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DefaultAction <Allow | AllowWithUrl | Block | BlockWithUrl>] [-DefaultURL <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，**Set-CsClientVersionConfiguration** Cmdlet 是用來修改 Identity 為 "site:Redmond" 的設定集合。在此範例中，Enabled 參數設為 False 以停用用戶端版本組態設定。

    Set-CsClientVersionConfiguration -Identity site:Redmond -Enabled $False

## 範例 2

範例 2 會修改組織目前所使用之所有用戶端版本組態設定的 DefaultUrl 屬性。為達成此目的，命令會先呼叫不含任何額外參數的 **Get-CsClientVersionConfiguration** Cmdlet，以傳回所有用戶端版本組態設定。然後再將該資訊管線傳送到 **Set-CsClientVersionConfiguration** Cmdlet，以將每個組態集合的 DefaultUrl 值設為 https://litwareinc.com/csclients。

    Get-CsClientVersionConfiguration | Set-CsClientVersionConfiguration -DefaultURL "https://litwareinc.com/csclients"

## 範例 3

範例 3 會針對 DefaultAction 目前設為 Block 的所有用戶端版本組態設定進行修改。為了執行此工作，命令會先使用 **Get-CsClientVersionConfiguration** Cmdlet，以傳回目前使用的所有用戶端版本組態設定。接著再將該資訊管線傳送到 **Where-Object** Cmdlet，這會只挑出 DefaultAction 屬性等於 "Block" 的項目。然後將篩選後的集合管線傳送到 **Set-CsClientVersionConfiguration** Cmdlet，並對集合中的每個項目執行兩個動作：1) 將 DefaultAction 設為 BlockWithUrl，以及 2) 將 DefaultUrl 設為 https://litwareinc.com/csclients。

    Get-CsClientVersionConfiguration | Where-Object {$_.DefaultAction -eq "Block"} | Set-CsClientVersionConfiguration -DefaultAction "BlockWithUrl" -DefaultURL "https://litwareinc.com/csclients"

## 詳細描述

Lync Server 在指定使用者可用於登入系統的用戶端軟體 (以及同樣重要的軟體版本號碼) 時，會為系統管理員提供更大的彈性。例如，沒有任何技術上的原因非要使用者使用 Lync Server 登入 Lync；也沒有任何技術限制不讓使用者使用 Microsoft Office Communicator 2007 R2 登入。

另一方面，也可能是一些非技術上的原因造成您不想要使用者使用 Office Communicator 2007 R2 登入。例如，Office Communicator 2007 R2 並不支援 Lync 中所有的功能，因此使用 Office Communicator 2007 R2 登入的使用者其使用經驗，會與使用 Lync 登入的使用者不同。這樣可能會造成使用者的困擾，也會造成服務台人員的困擾，因為他們必須提供多種不同用戶端應用程式的支援。

如果您的組織有這個問題，則可以運用用戶端版本篩選功能來指定可使用哪些用戶端應用程式登入 Lync Server。當您安裝 Lync Server 時，會安裝並啟用一組全域的用戶端版本組態設定。這些設定是用來判斷是否已啟用用戶端版本篩選。除了全域設定外，用戶端版本組態設定也會在網站範圍套用；在那些狀況下，網站設定會優先於全域設定。

**Set-CsClientVersionConfiguration** Cmdlet 可讓您修改現有的用戶端版本組態設定集合。

請注意，用戶端版本組態不是安全性功能。該技術可仰賴用戶端應用程式的自行報告，且不會嘗試確認應用程式是否真的是應用程式，而該應用程式的版本號碼就如其所聲明般。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsClientVersionConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClientVersionConfiguration"}

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultAction</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.DefaultAction</p></td>
<td><p>指出當使用者嘗試從無法在適當用戶端版本原則中找到其版本號碼的用戶端應用程式進行登入時，將會採取的行動。DefaultAction 必須設為下列其中一個值：</p>
<p>Allow。允許用戶端應用程式登入。</p>
<p>AllowWithUrl。將允許用戶端應用程式登入。此外，對使用者顯示的訊息方塊會包含網頁的 URL，使用者可在此下載已核准的用戶端應用程式。應將此網頁的 URL 指定為 DefaultUrl 屬性值。</p>
<p>Block。禁止用戶端應用程式登入。</p>
<p>BlockWithUrl。禁止用戶端應用程式登入。但是，對使用者顯示的「拒絕存取」訊息方塊將會包含網頁的 URL，使用者可在此下載已核准的用戶端應用程式。應將此網頁的 URL 指定為 DefaultUrl 屬性值。</p>
<p>如果 Enabled 屬性設為 False，則會忽略此屬性。將 Enabled 屬性設定為 False 之後，則不會進行任何用戶端版本篩選。</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultURL</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指定使用者可在該處下載已核准用戶端應用程式之網頁的 URL。如果有指定且 DefaultAction 設為 BlockWithURL，此 URL 將會出現在每次有使用者嘗試從不支援的用戶端應用程式登入時顯示的 [拒絕存取] 訊息方塊中。</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示用戶端版本篩選已啟用或已停用。如果 Enabled 屬性為 True，則伺服器會檢查嘗試登入之每個用戶端應用程式的版本號碼，然後伺服器會根據適當的用戶端版本原則允許或拒絕存取。如果將 Enabled 屬性設定為 False，則將允許任何可以登入之用戶端應用程式進行登入。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>代表要修改之用戶端版本組態設定的唯一識別碼。若要修改全域設定，請使用類似下列的語法：-Identity global。若要修改指派至網站範圍的設定，請使用類似下列的語法：&quot;site:Redmond&quot;。</p>
<p>若未加入此參數，<strong>Set-CsClientVersionConfiguration</strong> Cmdlet 會自動設定全域設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>ClientVersionPolicy 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration 物件。**Set-CsClientVersionConfiguration** Cmdlet 接受管線傳送的用戶端版本組態物件執行個體。

## 傳回類型

**Set-CsClientVersionConfiguration** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[New-CsClientVersionConfiguration](new-csclientversionconfiguration.md)  
[Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md)

