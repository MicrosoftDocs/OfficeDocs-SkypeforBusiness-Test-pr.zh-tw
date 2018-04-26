---
title: New-CsClientVersionConfiguration
TOCTitle: New-CsClientVersionConfiguration
ms:assetid: e7aac850-9e29-4d18-8929-74a89e9355cd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399029(v=OCS.15)
ms:contentKeyID: 49292650
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientVersionConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的用戶端版本組態設定集合。用戶端版本組態設定可指定 Lync Server 是否需要檢查登入系統之所有用戶端應用程式的版本號碼。如有啟用用戶端版本篩選，則用戶端應用程式存取系統的能力，將視相關用戶端版本原則中所設定的設定而定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsClientVersionConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-DefaultAction <Allow | AllowWithUrl | Block | BlockWithUrl>] [-DefaultURL <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立 Redmond 網站之用戶端版本組態設定的新集合。於此命令中，將 Enabled 參數設定為 False；這表示 Redmond 網站的用戶端篩選已遭停用。

    New-CsClientVersionConfiguration -Identity site:Redmond -Enabled $False

## 範例 2

範例 2 示範如何於記憶體中建立用戶端版本組態設定的新集合、修改該集合，然後將這些虛擬設定轉變為可套用至 Redmond 網站之設定的實際集合。為達成此目的，第一個命令會使用 **New-CsClientVersionConfiguration** Cmdlet 搭配 InMemory 參數，以建立只存在記憶體中且 Identity 為 site:Redmond 的設定集合。此集合會儲存於名為 $x 的變數中且只存在記憶體中。如果您終止 Windows PowerShell 工作階段或刪除變數 $x，這些用戶端版本組態設定將會消失，且永遠無法套用至 Redmond 網站。

於命令 2 中，會將虛擬設定的 DefaultAction 屬性值設定為 Block。於命令 3 中，會使用 **Set-CsClientVersionConfiguration** Cmdlet，將虛擬設定轉換為用戶端版本組態設定 (套用至 Redmond 網站) 的實際集合。

    $x = New-CsClientVersionConfiguration -Identity site:Redmond -InMemory
    $x.DefaultAction = "Block" 
    Set-CsClientVersionConfiguration -Instance $x

## 詳細描述

Lync Server 讓系統管理員有相當大的彈性空間可指定使用者用來登入系統的用戶端軟體 (以及同樣重要的該軟體版本號碼)。例如，沒有任何技術上的原因非要使用者使用 Lync Server 登入 Lync；也沒有任何技術限制不讓使用者使用 Microsoft Office Communicator 2007 R2 登入。

然而，也可能是一些非技術上的原因造成您不想要使用者使用 Office Communicator 2007 R2 登入。例如，Office Communicator 2007 R2 並不支援 Lync 中所有的功能，因此使用 Office Communicator 2007 R2 登入的使用者其使用經驗，會與使用 Lync 登入的使用者不同。這會對您的使用者造成一些困擾；也對服務台人員造成困擾，因為他們必須支援許多不同的用戶端應用程式。

如果您的組織會有這個問題，則可運用用戶端版本篩選功能來指定可使用哪些用戶端應用程式登入 Lync Server。當您安裝 Lync Server 時，會安裝並啟用一組全域的用戶端版本組態設定。這些設定會用於決定是否啟用用戶端版本篩選。

除了全域設定之外，**New-CsClientVersionConfiguration** Cmdlet 可讓您在網站範圍建立用戶端版本組態設定 當用戶端版本組態設定在網站範圍進行套用時，這些設定的優先順序會高於全域設定。例如，假設您已在全域範圍啟用了用戶端版本篩選，之後，為 Redmond 網站建立個別的設定集合，這是停用用戶端版本篩選的設定集合。在該案例中，其帳戶位於 Redmond 網站之所有使用者的用戶端版本篩選將會遭到停用。

但是請注意，匿名使用者僅會受到全域設定的影響。這是因為匿名使用者不會與網站產生關聯。

請注意，用戶端版本組態並非一個安全性功能。該技術可仰賴用戶端應用程式的自行報告，且不會嘗試確認應用程式是否真的是應用程式，而該應用程式的版本號碼就如其所聲明般。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsClientVersionConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientVersionConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示要指派給用戶端版本組態設定之新集合的唯一識別碼。由於您只能在網站範圍建立新集合，因此，Identity 一律是首碼 &quot;site:&quot; 加上網站名稱，例如 &quot;site:Redmond&quot;。請注意，若 Identity 為 site:Redmond 的設定集合已存在，則上述命令將會失敗。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultAction</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.DefaultAction</p></td>
<td><p>指出當使用者嘗試從無法在適當用戶端版本原則中找到其版本號碼的用戶端應用程式進行登入時，將會採取的行動。DefaultAction 必須設定為下列其中一個值：</p>
<p>Allow。將允許用戶端應用程式登入。</p>
<p>AllowWithUrl。將允許用戶端應用程式登入。此外，對使用者顯示的訊息方塊會包含網頁的 URL，使用者可在此下載已核准的用戶端應用程式。應將此網頁的 URL 指定為 DefaultUrl 屬性值。</p>
<p>Block。該用戶端應用程式將無法登入。</p>
<p>BlockWithUrl。該用戶端應用程式將無法登入。但是，對使用者顯示的「拒絕存取」訊息方塊將會包含網頁的 URL，使用者可在此下載已核准的用戶端應用程式。應將此網頁的 URL 指定為 DefaultUrl 屬性值。</p>
<p>如果將 Enabled 屬性設定為 False，則忽略此屬性。將 Enabled 屬性設定為 False 之後，則不會進行任何用戶端版本篩選。</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultURL</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指定使用者可在該處下載已核准用戶端應用程式之網頁的 URL。若指定並將 DefaultAction 設定為 BlockWithUrl，則此 URL 將會顯示於當使用者從未支援之用戶端應用程式登入時出現的「拒絕存取」訊息方塊中。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示用戶端版本篩選啟用或停用。如果將 Enabled 屬性設定為 True，伺服器將會檢查嘗試登入之每個用戶端應用程式的版本號碼；之後該伺服器將根據適當的用戶端版本原則允許或拒絕存取。如果將 Enabled 屬性設定為 False，則將允許任何可以登入之用戶端應用程式進行登入。</p>
<p>預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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

無。**New-CsClientVersionConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md)  
[Set-CsClientVersionConfiguration](set-csclientversionconfiguration.md)

