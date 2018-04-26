---
title: New-CsReportingConfiguration
TOCTitle: New-CsReportingConfiguration
ms:assetid: 2f033456-5c1c-4313-ab17-37038a412189
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204787(v=OCS.15)
ms:contentKeyID: 49290473
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsReportingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

在服務範圍建立新的報告組態設定集合。報告組態設定可指定用於存取 Lync Server 2013 監視報告的 URL。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsReportingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-ReportingUrl <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立指派給 Identity 為 service:MonitoringDatabase:atl-sql-001.litwareinc.com 之監控資料庫的新報告組態設定集合。在此範例中，ReportingUrl 屬性的值設為 "https://atl-sql-001.litwareinc.com/lync\_reports"。

    New-CsReportingConfiguration -Identity "service:MonitoringDatabase:atl-sql-001.litwareinc.com" -ReportingUrl "https://atl-sql-001.litwareinc.com/lync_reports"

## 詳細描述

報告組態設定可用於指定 Lync Server 監視報告的首頁。若您不使用監視報告，即無須修改報告組態設定。

若不知道監視報告首頁的 URL，可以執行下列動作加以判別：

1.  開啟監控資料庫所在之 SQL Server 執行個體上的 SQL Server Reporting Services Configuration Manager。

2.  在 Configuration Manager 中，按一下 \[報表管理員 URL\]，然後按一下監視報告的 URL。若是顯示兩組 URL，請點選使用 https 通訊協定的 URL。

3.  在 SQL Server Reporting Services 中，按一下 \[LyncServerReports\]。

4.  在 \[LyncServerReports\] 頁面中，按一下 \[報告首頁\]，以前往監控告的首頁。您可以複製該 URL，並在 CsReportingConfiguration Cmdlet 中使用之。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsReportingConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **New-CsReportingConfiguration** Cmdlet 所執行的功能。

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
<td><p>要與報告組態設定相關聯之監控資料庫的服務 Identity。例如：</p>
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
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照，而不需實際認可該物件為永久變更。如果您會將利用此參數呼叫之 Cmdlet 的輸出指派給變數，則可變更物件參照的屬性，然後呼叫此 Cmdlet 相符的 Set- Cmdlet 來認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportingUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>Lync Server 2013監視報告的 URL。</p></td>
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

無。**New-CsReportingConfiguration** Cmdlet 不接受管線傳送的資料。

## 傳回類型

**New-CsReportingConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.Reporting.ReportingConfiguration 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsReportingConfiguration](get-csreportingconfiguration.md)  
[Remove-CsReportingConfiguration](remove-csreportingconfiguration.md)  
[Set-CsReportingConfiguration](set-csreportingconfiguration.md)

