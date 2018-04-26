---
title: Set-CsReportingConfiguration
TOCTitle: Set-CsReportingConfiguration
ms:assetid: 8e7c8e8c-ab68-4f95-a58e-b04a9b2110ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205075(v=OCS.15)
ms:contentKeyID: 49291628
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsReportingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有報告組態設定集合的報告 URL。報告組態設定可用於指定用以存取 Lync Server 2013 監視報告的 URL。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsReportingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsReportingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-ReportingUrl <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改 Identity 為 service:MonitoringDatabase:atl-sql-002.litwareinc.com 之報告組態設定的報告 URL。在此範例中，報告 URL 會變更為 "https://atl-sql-002.litwareinc.com/lync\_reports"。

    Set-CsReportingConfiguration -Identity "service:MonitoringDatabase:atl-sql-002.litwareinc.com" -ReportingURL "https://atl-sql-002.litwareinc.com/lync_reports"

## 詳細描述

報告組態設定可用於指定 Lync Server 監視報告的首頁。若您不使用監視報告，即無須修改報告組態設定。

若不知道監視報告首頁的 URL，可以執行下列動作加以判別：

1.  開啟監控資料庫所在之 SQL Server 執行個體上的 SQL Server Reporting Services Configuration Manager。

2.  在 Configuration Manager 中，按一下 \[報表管理員 URL\]，然後按一下監視報告的 URL。若是顯示兩組 URL，請點選使用 https 通訊協定的 URL。

3.  在 SQL Server Reporting Services 中，按一下 \[LyncServerReports\]。

4.  在 \[LyncServerReports\] 頁面中，按一下 \[報告首頁\]，以前往監控告的首頁。您可以複製該 URL，並在 CsReportingConfiguration Cmdlet 中使用之。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsReportingConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Set-CsReportingConfiguration** Cmdlet 所執行的功能。

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
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改報告組態設定之監控資料庫的服務 Identity。例如：</p>
<p>-Identity &quot;Service:MonitoringDatabase:atl-sql-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參照傳遞給 Cmdlet，而非設定個別參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportingUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>Lync Server 2013 Monitoring Reports 的 URL。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Set-CsReportingConfiguration** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.Reporting.ReportingConfiguration 物件執行個體。

## 傳回類型

無。反之，**Set-CsReportingConfiguration** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.Reporting.ReportingConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsReportingConfiguration](get-csreportingconfiguration.md)  
[New-CsReportingConfiguration](new-csreportingconfiguration.md)  
[Remove-CsReportingConfiguration](remove-csreportingconfiguration.md)

