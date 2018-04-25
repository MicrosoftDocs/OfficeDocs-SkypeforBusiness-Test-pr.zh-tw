---
title: Invoke-CsQoEDatabasePurge
TOCTitle: Invoke-CsQoEDatabasePurge
ms:assetid: c4cae63a-b9dd-485b-8d53-2d81d353b7c3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205247(v=OCS.15)
ms:contentKeyID: 49292241
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsQoEDatabasePurge

 

_**上次修改主題的時間：** 2015-03-09_

手動清除經驗品質 (QoE) 資料庫中的記錄。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Invoke-CsQoEDatabasePurge -Identity <XdsIdentity> <COMMON PARAMETERS>

    Invoke-CsQoEDatabasePurge -SqlServerFqdn <String> [-SqlInstanceName <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -PurgeQoEDataOlderThanDays <Int32> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會從 atl-sql-001.litwareinc.com 的監控資料庫中，清除超過 10 天的所有 QoE 記錄。

    Invoke-CsQoEDatabasePurge -Identity "service:MonitoringDatabase:atl-sql-001.litwareinc.com" -PurgeQoEDataOlderThanDays 10

## 範例 2

範例 2 所示的命令是範例 1 所示命令的變化，但此範例會使用下列語法新增 Confirm 參數。

\-Confirm:$False

該語法會隱藏清除 QoE 記錄時所顯示的確認提示。

    Invoke-CsQoEDatabasePurge -Identity "service:MonitoringDatabase:atl-sql-001.litwareinc.com" -PurgeQoEDataOlderThanDays 10 -Confirm:$False

## 範例 3

範例 3 會從組織使用的所有監控 QoE 資料庫中，清除超過 10 天的所有 QoE 記錄。為達成此目的，範例中的第一個命令會使用 **Get-CsService** Cmdlet 搭配 MonitoringDatabase 參數，以傳回所有監控資料庫的集合。然後，此集合會管線傳送到 **ForEach-Object** Cmdlet。接著 **ForEach-Object** Cmdlet 會取出集合中的每一個資料庫，然後對該資料庫執行 **Invoke-CsQoEDatabasePurge** Cmdlet，以清除超過 10 天的所有經驗品質記錄。

    Get-CsService -MonitoringDatabase | Invoke-CsQoEDatabasePurge -PurgeQoEDataOlderThanDays 10 -Confirm:$False

## 詳細描述

經驗品質 (QoE) 數據可用以追蹤組織所撥打之音訊與視訊通話的品質，包括遺失的網路封包數、背景雜訊與抖動量 (封包延遲差異)。這些數據會儲存在不同於資料 (例如通話詳細記錄) 儲存的資料庫，以便您可以不影響其他資料記錄而啟用或停用 QoE。

經驗品質記錄會儲存在 SQL Server 資料庫 LcsQoEMetrics 中。隨著時間的更迭，此資料庫可能會變得極大。有鑑於此，Lync Server 為系統管理員提供下列兩種方法來清除資料庫中的舊記錄：1) 將 Lync Server 設為每天自動刪除較舊的封存記錄；及/或 2) 隨時使用 **Invoke-CsQoEDatabasePurge** Cmdlet 來刪除 LcsQoEMetrics 資料庫中的經驗品質記錄 (**Invoke-CsQoEDatabasePurge** Cmdlet 會呼叫 SQL Server 預存程序 QoePurgeOutdatedReports 來執行此動作)。

當您呼叫 **Invoke-CsQoEDatabasePurge** Cmdlet 時，必須指定用以儲存 QoE 記錄之監控資料庫的服務位置 (例如 MonitoringDatabase:atl-sql-001.litwareinc.com)，另外還須指定刪除封存記錄前至少應保留的時間 (天)。例如，若指定了 10 天的最短保留時間，則資料庫中所有保留時間長於 10 天的 QoE 記錄皆會予以刪除。

請注意，即使已針對指定的資料庫停用清除功能 (亦即，已將 QoE 組態設定中的 EnablePurging 屬性設為 False)，仍會刪除這些記錄。EnablePurging 屬性只能控制封存記錄的自動清除功能，對於 **Invoke-CsQoEDatabasePurge** Cmdlet 沒有影響。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示中執行下列命令

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsQoEDatabasePurge"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Invoke-CsQoEDatabasePurge** Cmdlet 所執行的功能。

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
<td><p><em>PurgeQoEDataOlderThanDays</em></p></td>
<td><p>必要</p></td>
<td><p>System.Int32</p></td>
<td><p>指定從資料庫清除 QoE 記錄之前的記錄存留期 (以天數為單位)，大於此值的所有記錄都將遭到刪除。</p>
<p>PurgeQoEDataOlderThanHours 可設為介於 1 和 2147483647 (含) 之間的任何整數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>QoE 資料庫所在之電腦的完整網域名稱。例如：</p>
<p>-SqlServerFqdn &quot;atl-sql-001.litwareinc.com&quot;</p>
<p>請注意，請勿在同一個命令中同時使用 Identity 參數與 SqlServerFqdn 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>QoE 資料庫的 SQL Server 執行個體名稱。例如：</p>
<p>-SqlInstanceName &quot;archinst&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Invoke-CsQoEDatabasePurge** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.Xds.DisplayMonitoringDatabase\#Decorated 類別執行個體。

## 傳回類型

**Invoke-CsQoEDatabasePurge** Cmdlet 會傳回 Microsoft.Rtc.Management.Purge.QoEDataPurgeStatistics 類別的執行個體。

## 請參閱

#### 其他資源

[New-CsQoEConfiguration](new-csqoeconfiguration.md)  
[Set-CsQoEConfiguration](set-csqoeconfiguration.md)

