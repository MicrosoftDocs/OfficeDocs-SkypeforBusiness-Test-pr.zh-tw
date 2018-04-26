---
title: Set-CsMonitoringServer
TOCTitle: Set-CsMonitoringServer
ms:assetid: 2c6d6660-7e41-4c56-9e04-27c3d1ea3b95
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425776(v=OCS.15)
ms:contentKeyID: 49290444
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsMonitoringServer

 

_**上次修改主題的時間：** 2015-03-09_

可讓您設定監控伺服器資料庫和報告套件的新位置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsMonitoringServer [-Identity <XdsGlobalRelativeIdentity>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-MonitoringDatabase <String>] [-ReportingUrl <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會設定 監控伺服器 報告套件的新 URL。

    Set-CsMonitoringServer -Identity "MonitoringServer:atl-cs-001.litwareinc.com" -ReportingUrl "https://atl-cs-001.litwareinc.com/reports"

## 詳細描述

監控伺服器 提供兩個重要功能。第一，它可讓您維護在組織中使用 Enterprise Voice 之方法及頻率的資訊。此資訊是使用通話詳細記錄 (CDR) 進行追蹤；該記錄會詳細說明撥打電話者、撥打對象，以及通話持續的長度。(系統不會記錄實際交談內容)。此外，您也可以使用 監控伺服器 追蹤 Enterprise Voice 通話的經驗品質 (QoE) 資料。顧名思義，經驗品質資料提供通話品質的資訊，並測量封包遺失、通話品質降低、網路位元速率及「抖動」之類的項目。

當您安裝 監控伺服器 時，必須指定用來儲存 CDR 和 QoE 資料之 SQL Server 資料庫的位置。或者，您也可以安裝 SQL Server Reporting Services 和 監控伺服器 報告套件；這兩個項目可讓您存取產生標準監視報告的網站。

一般的規則是，在安裝並設定 監控伺服器 之後，就不需要變更後端資料庫或報告 URL 的位置。不過，如果您需要變更這些項目其中之一 (或兩者) 的位置，也可以藉由執行 **Set-CsMonitoringServer** Cmdlet 來達成。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsMonitoringServer** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsMonitoringServer"}

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
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要修改的監控伺服器服務位置。例如：-Identity &quot;MonitoringServer:atl-cs-001.litwareinc.com&quot;。您可以使用以下命令擷取所有 監控伺服器 的 Identity：</p>
<p>Get-CsService –MonitoringServer | Select-Object Identity。</p>
<p>請注意，您可以省略首碼 &quot;MonitoringServer:&quot;指定監控伺服器時，您可以省略首碼 &quot;MediationServer:&quot;。例如：-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>MonitoringDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>新 監控伺服器 資料庫的服務位置。例如：-MonitoringDatabase &quot;MonitoringDatabase:atl-sql-001.litwareinc.com&quot;。請確認您使用的是資料庫存放的服務位置，而不是 SQL Server 路徑名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportingUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>監控伺服器 報告的 URL。請注意，除非安裝 SQL Server Reporting Services 和 監控伺服器 報告套件，否則無法使用這些報告。</p></td>
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

無。**Set-CsMonitoringServer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsMonitoringServer** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.Xds.DisplayMonitoringServer 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsService](get-csservice.md)

