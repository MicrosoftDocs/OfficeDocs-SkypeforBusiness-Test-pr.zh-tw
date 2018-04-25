---
title: Get-CsReportingConfiguration
TOCTitle: Get-CsReportingConfiguration
ms:assetid: e777a154-354a-49da-8140-79f80416bc49
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205356(v=OCS.15)
ms:contentKeyID: 49292645
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsReportingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織使用之報告組態設定的資訊。報告組態設定可用於指定用以存取 Lync Server 2013 監視報告的 URL。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsReportingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsReportingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織目前使用之所有報告組態設定的資訊。

    Get-CsReportingConfiguration

## 範例 2

範例 2 會傳回單一報告組態設定 (即 Identity 為 "Service:MonitoringDatabase:atl-sql-001.litwareinc.com" 的設定) 集合的資訊。

    Get-CsReportingConfiguration -Identity "Service:MonitoringDatabase:atl-sql-001.litwareinc.com"

## 範例 3

範例 3 會傳回 Identity 結尾為 ".litwareinc.com" 之所有報告組態設定的資訊。為達此目的，命令會使用 Filter 參數和篩選值 "\*.litwareinc.com"。

    Get-CsReportingConfiguration -Filter "*.litwareinc.com"

## 範例 4

範例 4 會傳回報告 URL 其任何部分包含字串值 "\_ARCHINST" 之所有報告組態設定的資訊。為達成此目的，命令會先使用 **Get-CsReportingConfiguration** Cmdlet，以傳回目前使用的所有報告組態設定集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 ReportingUrl 包含 (-like) 字串值 "\_ARCHINST" 的設定。

    Get-CsReportingConfiguration | Where-Object {$_.ReportingUrl -like "*_ARCHINST*"}

## 詳細描述

報告組態設定可用於指定 Lync Server 監視報告的首頁。若您不使用監視報告，即無需修改報告組態設定。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsReportingConfiguration

**Lync Server 控制台：**Lync Server 控制台不提供 **Get-CsReportingConfiguration** Cmdlet 所執行的功能。

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您在指定要傳回的報告組態設定時使用萬用字元。例如，下列語法會傳回在服務範圍設定的所有設定：</p>
<p>-Filter &quot;service:*&quot;</p>
<p>請注意，您不能在同一個命令中同時使用 Filter 和 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要與報告組態設定相關聯之監控資料庫的服務識別。例如：</p>
<p>-Identity &quot;Service:MonitoringDatabase:atl-sql-001.litwareinc.com&quot;</p>
<p>若未在命令中加入 Identity 參數或 Filter 參數，則 <strong>Get-CsReportingConfiguration</strong> Cmdlet 會傳回組織使用的所有報告組態設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取報告組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsReportingConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsReportingConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.Reporting.ReportingConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsReportingConfiguration](new-csreportingconfiguration.md)  
[Remove-CsReportingConfiguration](remove-csreportingconfiguration.md)  
[Set-CsReportingConfiguration](set-csreportingconfiguration.md)

