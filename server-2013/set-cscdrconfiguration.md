---
title: Set-CsCdrConfiguration
TOCTitle: Set-CsCdrConfiguration
ms:assetid: 977f0d3e-796b-43a3-bc0c-82ea91741c52
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398774(v=OCS.15)
ms:contentKeyID: 49291734
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCdrConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的通話詳細記錄 (CDR) 設定集合。CDR 可讓您追蹤對等立即訊息工作階段、Voice over Internet Protocol (VoIP) 電話及會議電話等的使用狀況。這項使用狀況資料包括了誰撥電話給誰、撥話時間，以及通話時間長度等資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsCdrConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCdrConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableCDR <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-KeepCallDetailForDays <UInt32>] [-KeepErrorReportForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例1 會設定清除舊記錄的時間。在此範例中，該時間設為 23 (24 小時制的 11:00 P.M.)。Identity 參數可用來確保只對 Identity 為 site:Redmond 的 CDR 設定進行這些變更。

    Set-CsCdrConfiguration -Identity site:Redmond -PurgeHourOfDay 23 

## 範例 2

範例 2 是範例 1 所示命令的變化；此範例會針對組織中目前使用的每個 CDR 組態設定集合，修改 PurgeHourOfDay 屬性。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsCdrConfiguration** Cmdlet，以傳回目前所使用之所有 CDR 設定的集合。然後再將該集合管線傳送至 **Set-CsCdrConfiguration** Cmdlet，以將集合中每個項目之 PurgeHourOfDay 屬性的值變更為 11:00 PM (23)。

    Get-CsCdrConfiguration | Set-CsCdrConfiguration -PurgeHourOfDay 23 

## 範例 3

範例 3 所示是範例 1 所用命令的另一種變化。此範例會變更所有在網站範圍設定之 CDR 設定的 PurgeHourOfDay 屬性。為了執行此工作，命令會先呼叫 **Get-CsCdrConfiguration** Cmdlet 並搭配 Filter 參數；篩選值 "site:\*" 可確保只會傳回 Identity 開頭為字串值 "site:" 的 CDR 設定。然後再將篩選後的集合管線傳送到 **Set-CsCdrConfiguration** Cmdlet，以變更集合中每個項目的 PurgeHourOfDay 屬性。

    Get-CsCdrConfiguration -Filter "site:*"| Set-CsCdrConfiguration -PurgeHourOfDay 23

## 詳細描述

通話詳細記錄 (CDR) 讓您能夠追蹤 Lync Server 功能的使用狀況，這些功能包括 Voice over Internet Protocol (VoIP) 通話、立即訊息 (IM)、檔案傳輸、音訊/視訊 (A/V) 會議，以及應用程式分享工作階段。CDR (只有在您有部署監視服務時才能使用) 會保留使用狀況資訊：它會記錄通話方、通話長度、是否傳輸任何檔案等資訊。但是，CDR 不會記錄通話本身。

CDR 也會追蹤通話錯誤資訊：點對點工作階段與會議電話的詳細診斷資料。

做為系統管理員，您可以決定是否要在組織中使用 CDR；假設已部署監控服務，您就可以輕鬆地啟用或停用 CDR。此外，您還可以依全域 (在整個組織啟用或停用 CDR) 或個別網站的基礎來進行此決策。例如，您可以在 Redmond 網站使用 CDR，但在 Paris 網站不使用 CDR。

系統管理員也可以管理 CDR 資料庫；例如，您可以指定在從該資料庫中清除 CDR 記錄之前要保留該記錄的天數。諸如這類的變更可以使用 **Set-CsCdrConfiguration** Cmdlet 來進行。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsCdrConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCdrConfiguration"}

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
<td><p><em>EnableCDR</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否啟用 CDR。預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePurging</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否要從 CDR 資料庫定期刪除 CDR 記錄。若為 True (預設值)，則會在過了 KeepCallDetailForDays (適用於 CDR 記錄) 和 KeepErrorReportForDays (適用於 CDR 錯誤) 內容指定的期間之後刪除記錄。若為 False，則會無限期保留 CDR 記錄。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>指派給 CDR 組態設定集合的唯一識別碼。若要參照全域設定，請使用下列語法：-Identity global。若要參考在此網站範圍設定的集合，請使用如下語法：-Identity site:Redmond。請注意，指定 Identity 時不能使用萬用字元。</p>
<p>如果省略此參數，則 <strong>Set-CsCdrConfiguration</strong> Cmdlet 會修改全域設定。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>CdrSettings 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepCallDetailForDays</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示在 CDR 資料庫保留 CDR 記錄的天數；任何超過指定天數的記錄都將自動刪除。(請注意，只有在 EnablePurging 屬性已設為 True 時，才會進行清除)。</p>
<p>您可以將此屬性設為任何介於 1 與 2562 天 (大約 7 年) 的整數值。預設值為 60。</p></td>
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
<td><p>表示從 CDR 資料庫刪除過期記錄的當地時間。時間是以 24 小時制指定，0 代表午夜 (12:00 A.M.)，而 23 則代表 11:00 P.M.。請注意，您只能指定每天中的小時；這表示，雖然您可以將清除作業排定在 4:00 A.M. 進行，但無法將清除作業排定在 4:30 A.M. 或 4:15 A.M. 進行。預設值為 2 (2:00 A.M.)。建議在下班時間進行清除作業。</p>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings。**Set-CsCdrConfiguration** Cmdlet 接受管線傳送的通話詳細記錄組態物件輸入。

## 傳回類型

**Set-CsCdrConfiguration** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CDRSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)

