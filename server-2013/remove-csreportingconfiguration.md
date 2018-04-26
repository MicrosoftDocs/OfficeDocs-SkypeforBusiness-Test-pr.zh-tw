---
title: Remove-CsReportingConfiguration
TOCTitle: Remove-CsReportingConfiguration
ms:assetid: 17cc1865-4bd9-4630-9947-2c432d1203b3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204711(v=OCS.15)
ms:contentKeyID: 49290216
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsReportingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除現有報告組態設定的集合。報告組態設定可用於指定 Lync Server 2013 監視報告安裝的 URL。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsReportingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會移除 Identity 為 service:MonitoringDatabase:atl-sql-002.litwareinc.com 的報告組態設定。

    Remove-CsReportingConfiguration -Identity "service:MonitoringDatabase:atl-sql-002.litwareinc.com"

## 範例 2

範例 2 會移除組織所使用的所有報告組態設定。為達成此目的，命令會先使用 **Get-CsReportingConfiguration** Cmdlet 傳回所有報告組態設定的集合。然後，此集合會管線傳送到 **Remove-CsReportingConfiguration** Cmdlet，移除集合中的每個項目。

    Get-CsReportingConfiguration | Remove-CsReportingConfiguration

## 範例 3

範例 3 所示的命令會刪除報告 URL 設為 https://atl-sql-002.litwareinc.com/lync\_reports 的任何報告組態設定。為了執行此工作，命令會先使用 **Get-CsReportingConfiguration** Cmdlet 傳回目前所使用的所有報告組態設定。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 ReportingURL 屬性等於 https://atl-sql-002.litwareinc.com/lync\_reports 的設定。接著將篩選後的集合管線傳送到 **Remove-CsReportingConfiguration** Cmdlet，以移除集合中的每一個項目。

    Get-CsReportingConfiguration | Where-Object {$_.ReportingUrl -eq "https://atl-sql-002.litwareinc.com/lync_reports" | Remove-CsReportingConfiguration

## 詳細描述

報告組態設定可用於指定 Lync Server 監視報告的首頁。若您不使用監視報告，即無須修改報告組態設定。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsReportingConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Remove-CsReportingConfiguration** Cmdlet 所執行的功能。

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
<td><p>要移除報告組態設定之監控資料庫的服務 Identity。例如：</p>
<p>-Identity &quot;Service:MonitoringDatabase:atl-sql-001.litwareinc.com&quot;</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Remove-CsReportingConfiguration** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.Reporting.ReportingConfiguration 物件執行個體。

## 傳回類型

無。反之，**Remove-CsReportingConfiguration** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.Reporting.ReportingConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsReportingConfiguration](get-csreportingconfiguration.md)  
[New-CsReportingConfiguration](new-csreportingconfiguration.md)  
[Set-CsReportingConfiguration](set-csreportingconfiguration.md)

