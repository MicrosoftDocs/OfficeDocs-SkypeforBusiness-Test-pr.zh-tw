---
title: Test-CsDatabase
TOCTitle: Test-CsDatabase
ms:assetid: 4165f1e1-fe64-45e7-a13f-f23c0205f386
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204839(v=OCS.15)
ms:contentKeyID: 49290721
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsDatabase

 

_**上次修改主題的時間：** 2015-03-09_

測試 Lync Server 2013資料庫的組態。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Test-CsDatabase -LocalService <SwitchParameter> <COMMON PARAMETERS>

    Test-CsDatabase -CentralManagementDatabase <SwitchParameter> [-SqlInstanceName <String>] [-SqlServerFqdn <Fqdn>] <COMMON PARAMETERS>

    Test-CsDatabase -ConfiguredDatabases <SwitchParameter> -SqlServerFqdn <Fqdn> <COMMON PARAMETERS>

    Test-CsDatabase -DatabaseType <Application | Archiving | Monitoring | User | Provision | CentralAdmin | Lyss | Registrar | Edge | PersistentChat | PersistentChatCompliance | CentralMgmt> -SqlServerFqdn <Fqdn> [-SqlInstanceName <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會驗證中央管理資料庫的組態。

    Test-CsDatabase -CentralManagementDatabase

## 範例 2

範例 2 會驗證安裝在 atl-sql-001.litwareinc.com 電腦上的所有 Lync Server 資料庫。

    Test-CsDatabase -ConfiguredDatabases -SqlServerFqdn "atl-sql-001.litwareinc.com"

## 範例 3

在範例 3 中，只會驗證安裝在 atl-sql-001.litwareinc.com 電腦上的封存資料庫。請注意，會包含 SqlInstanceName 參數來指定封存資料庫所在的 SQL Server 執行個體 (Archinst)。

    Test-CsDatabase -DatabaseType "Archiving" -SqlServerFqdn "atl-sql-001.litwareinc.com" -SqlInstanceName "archinst"

## 範例 4

範例 4 所示的命令會驗證本機電腦上所安裝的資料庫。

    Test-CsDatabase -LocalService

## 詳細描述

**Test-CsDatabase** Cmdlet 可驗證一或多個 Lync Server 2013 資料庫的連線能力。 **Test-CsDatabase** Cmdlet 執行時，會讀取 Lync Server 拓撲，並嘗試連接每個相關的資料庫，然後回報每項連接作業為成功或失敗。若連線成功，此 Cmdlet 亦會回報資料庫名稱、SQL Server 版本資訊與所安裝之鏡像資料庫的位置等資訊。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsDatabase"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Test-CsDatabase** Cmdlet 所執行的功能。

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
<td><p><em>CentralManagementDatabase</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>測試中央管理資料庫的組態。此參數無法與 ConfiguredDatabases 參數或 DatabaseType 參數搭配使用。</p></td>
</tr>
<tr class="even">
<td><p><em>ConfiguredDatabases</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>測試安裝在指定電腦上之所有 Lync Server 資料庫的組態。當您使用 ConfiguredDatabases 參數時，必須包含 SqlServerFqdn 參數。此外，請勿在使用 CentralManagementDatabase 或 DatabaseType 參數的命令中使用此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>DatabaseType</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.DatabaseNameType</p></td>
<td><p>要驗證之資料庫的類型。允許的值為：</p>
<p>DatabaseType 的有效值為：</p>
<p>Application</p>
<p>Archiving</p>
<p>CentralAdmin</p>
<p>CentralMgmt</p>
<p>Edge</p>
<p>Lyss</p>
<p>Monitoring</p>
<p>PersistentChat</p>
<p>PersistentChatCompliance</p>
<p>Provision</p>
<p>Registrar</p>
<p>User</p></td>
</tr>
<tr class="even">
<td><p><em>LocalService</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>驗證所有由任一 Lync Server 服務使用的資料庫都安裝在本機電腦上。這不只包括本機安裝的資料庫，還包括安裝在遠端電腦上的資料庫；前提是這些資料庫都是由一或多個本機服務使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>安裝所要驗證之資料庫的電腦的完整網域名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：</p>
<p>-Report &quot;C:\Logs\TestDatabases.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>安裝所要驗證之資料庫的 SQL Server 執行個體。例如：</p>
<p>-SqlInstanceName &quot;rtc&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsDatabase** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsDatabase** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsDatabaseMirrorState](get-csdatabasemirrorstate.md)  
[Get-CsService](get-csservice.md)  
[Get-CsUserDatabaseState](get-csuserdatabasestate.md)

