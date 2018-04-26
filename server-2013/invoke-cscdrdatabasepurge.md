---
title: Invoke-CsCdrDatabasePurge
TOCTitle: Invoke-CsCdrDatabasePurge
ms:assetid: 95eb0faf-49dc-4afb-b98c-15735a4cab13
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205113(v=OCS.15)
ms:contentKeyID: 49291721
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsCdrDatabasePurge

 

_**上次修改主題的時間：** 2015-03-09_

手動清除通話詳細記錄 (CDR) 資料庫中的記錄。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Invoke-CsCdrDatabasePurge -Identity <XdsIdentity> <COMMON PARAMETERS>

    Invoke-CsCdrDatabasePurge -SqlServerFqdn <String> [-SqlInstanceName <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -PurgeCallDetailDataOlderThanDays <Int32> -PurgeDiagnosticDataOlderThanDays <Int32> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會從 atl-sql-001.litwareinc.com 監控資料庫中刪除已留存超過 10 天的所有記錄 (通話詳細記錄及診斷記錄都包括在內)。

    Invoke-CsCdrDatabasePurge -Identity "service:MonitoringDatabase:atl-sql-001.litwareinc.com" -PurgeCallDetailDataOlderThanDays 10 -PurgeDiagnosticDataOlderThanDays 10

## 範例 2

範例 2 所示的命令是範例 1 所示命令的變化，但此範例會使用下列語法新增 Confirm 參數。

\-Confirm:$False

該語法會隱藏清除 CDR 記錄時所出現的確認提示。

    Invoke-CsCdrDatabasePurge -Identity "service:MonitoringDatabase:atl-sql-001.litwareinc.com" -PurgeCallDetailDataOlderThanDays 10 -PurgeDiagnosticDataOlderThanDays 10 -Confirm:$False

## 範例 3

範例 3 會從組織正在使用的所有 CDR 資料庫中，清除已留存 10 天以上的所有記錄。為達成此目的，範例中的第一個命令會使用 **Get-CsService** Cmdlet 搭配 MonitoringDatabase 參數，以傳回所有監控資料庫的集合。然後，此集合會管線傳送到 **ForEach-Object** Cmdlet。接者， **ForEach-Object** Cmdlet 會針對集合中的每個資料庫執行 **Invoke-CsCdrDatabasePurge** Cmdlet，以清除已留存 10 天以上的所有通話詳細記錄。

    Get-CsService -MonitoringDatabase | ForEach-Object {Invoke-CsCdrDatabasePurge -Identity $_.Identity -PurgeCallDetailDataOlderThanDays 10 -PurgeDiagnosticDataOlderThanDays 10 -Confirm:$False}

## 詳細描述

通話詳細記錄 (CDR) 可讓您追蹤 Lync Server 功能 (如 Voice over IP (VoIP) 電話、立即訊息 (IM)、檔案傳輸、音訊/視訊 (A/V) 會議及應用程式共用工作階段) 的使用狀況。CDR 可以保存使用狀況的資訊，包括記錄參與的通話方、通話長度，以及有無任何檔案傳輸活動等等的資訊。但 CDR 不會記錄通話本身。

CDR 也會追蹤通話錯誤資訊：點對點工作階段與會議電話的詳細診斷資料。

通話詳細記錄會儲存在 SQL Server 資料庫 LcsCDR 中。隨著時間的更迭，此資料庫可能會變得極大。有鑑於此， Lync Server 為系統管理員提供下列兩種方法清除資料庫中的舊記錄：1) 將 Lync Server 設定為每天自動刪除較舊的 CDR 記錄；以及/或 2) 隨時使用 **Invoke-CsCdrDatabasePurge** Cmdlet 刪除 LcsLog 資料庫中的 CDR 記錄 ( **Invoke-CsCdrDatabasePurge** Cmdlet 的做法是呼叫 SQL Server 的預存程序 RtcCleanupDB)。

當您呼叫 **Invoke-CsCdrDatabasePurge** Cmdlet 時，必須指定用以儲存 CDR 記錄之監控資料庫的服務位置 (例如 MonitoringDatabase:atl-sql-001.litwareinc.com)，另外還須指定刪除通話詳細資料與診斷資料記錄前至少應保留的時間 (天)。例如，若指定了 10 天的最短保留時間，則資料庫中所有保留時間長於 10 天的通話詳細記錄皆會予以刪除。

請注意，即使指定的資料庫已停用清除功能 (亦即，CDR 組態設定中的 EnablePurging 屬性設為 False)，仍會刪除這些記錄。EnablePurging 屬性只可控制 CDR 記錄的自動清除功能，對於 **Invoke-CsCdrDatabasePurge** Cmdlet 沒有影響。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsCdrDatabasePurge"}

**Lync Server 控制台：** **Invoke-CsCdrDatabasePurge** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>要清除之監控資料庫的服務識別。您可以執行此命令以擷取監控資料庫的識別：</p>
<p>Get-CsService –MonitoringDatabase</p>
<p>請注意，請勿在同一個命令中同時使用 Identity 參數與 SqlServerFqdn 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>PurgeCallDetailDataOlderThanDays</em></p></td>
<td><p>必要</p></td>
<td><p>System.Int32</p></td>
<td><p>指定要從資料庫中清除之通話詳細記錄的存留時間 (以天數為單位)；存留時間超過此值的任何記錄都會遭刪除。通話詳細記錄代表使用者/工作階段報告。其不同於診斷資料報告，診斷資料報告是由 Lync 2013 之類的用戶端應用程式所上傳的診斷記錄。</p>
<p>PurgeCallDetailDataOlderThanDays 可設為 1 到 2147483647 的任何整數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeDiagnosticDataOlderThanDays</em></p></td>
<td><p>必要</p></td>
<td><p>System.Int32</p></td>
<td><p>指定要從資料庫中清除之診斷資料記錄的存留時間 (以天數為單位)；存留時間超過此值的任何記錄都會遭刪除。診斷資料報告是由 Lync 2013 之類的用戶端應用程式所上傳的診斷記錄。</p>
<p>PurgeDiagnosticDataOlderThanHours 可設為 1 到 2147483647 的任何整數值。</p></td>
</tr>
<tr class="even">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>CDR 資料庫所在之電腦的完整網域名稱。例如：</p>
<p>-SqlServerFqdn &quot;atl-sql-001.litwareinc.com&quot;</p>
<p>請注意，請勿在同一個命令中同時使用 Identity 參數與 SqlServerFqdn 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>CDR 資料庫的 SQL Server 執行個體名稱。例如：</p>
<p>-SqlInstanceName &quot;archinst&quot;</p></td>
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

**Invoke-CsCdrDatabasePurge** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.Xds.DisplayMonitoringDatabase\#Decorated 類別執行個體。

## 傳回類型

**Invoke-CsCdrDatabasePurge** Cmdlet 會傳回 Microsoft.Rtc.Management.Purge.CdrDataPurgeStatistics 類別的執行個體。

## 請參閱

#### 其他資源

[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

