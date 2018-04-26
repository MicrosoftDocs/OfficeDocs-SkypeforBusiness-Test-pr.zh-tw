---
title: New-CsCdrConfiguration
TOCTitle: New-CsCdrConfiguration
ms:assetid: e5890ac3-7a6c-4609-a866-84c39b76d3a9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399018(v=OCS.15)
ms:contentKeyID: 49292621
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsCdrConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的通話詳細記錄 (CDR) 設定集合。CDR 可讓您追蹤對等立即訊息工作階段、Voice over Internet Protocol (VoIP) 電話及會議電話等的使用狀況。這項使用狀況資料包括了誰撥電話給誰、撥話時間，以及通話時間長度等資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsCdrConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableCDR <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-KeepCallDetailForDays <UInt32>] [-KeepErrorReportForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 中的命令會使用 **New-CsCdrConfiguration** Cmdlet 建立一組 Identity 為 site:Redmond 的新 CDR 設定。除了 Identity 為 site:Redmond 之外，新的設定也將 EnableCDR 屬性設定為 False。因為網站設定的優先順序高於全域設定，這表示 CDR 將不會用於 Redmond 網站中，無論是否已在全域範圍啟用 CDR。

    New-CsCdrConfiguration -Identity site:Redmond -EnableCDR $False

## 範例 2

範例 2 會使用 InMemory 參數，示範如何建立一開始只存在於記憶體中的新 CDR 組態設定集合。為達成此目的，範例會先使用 **New-CsCdrConfiguration** Cmdlet 搭配 InMemory 參數，以建立 Identity 為 site:Redmond 之設定的虛擬集合。此虛擬集合會儲存於變數 $x 中；如果未將集合儲存於變數中，則會建立該集合，然後隨即消失。

建立虛擬集合之後，第 2 行所示的命令會將 EnableCDR 屬性值設為 False ($False)。在第 3 行中，接著會使用 **Set-CsCdrConfiguration** Cmdlet，以將虛擬集合 $x 轉換為要套用至 Redmond 網站之 CDR 組態設定的真實集合。若未呼叫 **Set-CsCdrConfiguration** Cmdlet，則虛擬集合將會在終止 Windows PowerShell 工作階段或變數 $x 遭到刪除的同時隨即消失。

    $x = New-CsCdrConfiguration -Identity site:Redmond -InMemory
    $x.EnableCDR = $False
    Set-CsCdrConfiguration -Instance $x

## 詳細描述

通話詳細記錄 (CDR) 讓您能夠追蹤 Lync Server 功能的使用狀況，這些功能包括 Voice over IP (VoIP) 通話、立即訊息、檔案傳輸、音訊/視訊 (A/V) 會議，以及應用程式分享工作階段。CDR (只有在您有部署監視服務時才能使用) 會保持記錄使用狀況資訊：它會記錄通話方、通話長度、是否傳輸任何檔案等資訊 (但 CDR 不會記錄通話本身)。

CDR 也會追蹤通話錯誤資訊：點對點工作階段與會議電話的詳細診斷資料。

做為系統管理員，您可以決定是否要在組織中使用 CDR；如果已部署監控服務，您就可以輕鬆地啟用或停用 CDR。此外，您還可以依全域 (在整個組織啟用或停用 CDR) 或個別網站的基礎來進行此決策；例如，您可以在 Redmond 網站使用 CDR，但在 Paris 網站不使用 CDR。

**New-CsCdrConfiguration** Cmdlet 可讓您在網站範圍建立新的 CDR 設定集合 (無法在全域範圍建立新的設定)。請注意，每個網站只能主控一個單一的 CDR 設定集合。這表示如果 Redmond 網站已具有一組 CDR 組態集合，則您無法建立該網站的新集合。如果您嘗試這麼做，則命令會失敗。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsCdrConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsCdrConfiguration"}

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
<td><p>代表要指派給 CDR 組態設定之新集合的唯一識別碼。由於您只能在網站範圍建立新集合，因此，Identity 一律是首碼 &quot;site:&quot; 加上網站名稱，例如 &quot;site:Redmond&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCDR</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否啟用 CDR。預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePurging</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否要從 CDR 資料庫定期刪除 CDR 記錄。若為 True (預設值)，則會在過了 KeepCallDetailForDays (CDR 紀錄) 和 KeepErrorReportForDays (CDR 錯誤) 屬性指定的時段之後刪除記錄。若為 False，則會無限期保留 CDR 記錄。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepCallDetailForDays</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示在 CDR 資料庫保留 CDR 記錄的天數；任何超過指定天數的記錄都將自動刪除。(請注意，只有在 EnablePurging 屬性已設為 True 時，才會進行清除)。</p>
<p>KeepCallDetailForDays 可設定為任何介於 1 至 2562 天 (大約 7 年) 的整數值。預設值為 60。</p></td>
</tr>
<tr class="even">
<td><p><em>KeepErrorReportForDays</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示保留 CDR 錯誤報告的天數；任何超過指定天數的報告都將自動刪除。CDR 錯誤報告是由 Lync 2013 這類用戶端應用程式所上載的診斷報告。</p>
<p>您可以將此屬性設為任何介於 1 與 2562 天 (大約 7 年) 的整數值。預設值為 60。</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示從 CDR 資料庫刪除過期記錄的當地時間。時間是以 24 小時制指定，0 代表午夜 (12:00 AM)，而 23 則代表 11:00 PM。請注意，您只能指定一天中的小時。這表示您可以排程要在 4:00 AM 執行清除，但無法將之排程為在 4:30 AM 或 4:15 AM 執行。預設值為 2 (2:00 AM)。建議在下班時間進行清除作業。</p>
<p>只有在 EnablePurging 屬性設為 True 時，才會進行資料庫清除作業。</p></td>
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

無。**New-CsCdrConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

