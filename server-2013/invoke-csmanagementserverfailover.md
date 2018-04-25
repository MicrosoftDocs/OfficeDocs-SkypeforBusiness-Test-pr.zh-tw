---
title: Invoke-CsManagementServerFailover
TOCTitle: Invoke-CsManagementServerFailover
ms:assetid: 060ab02a-1267-4b35-bc2b-6a4a35616be0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204647(v=OCS.15)
ms:contentKeyID: 49289969
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsManagementServerFailover

 

_**上次修改主題的時間：** 2015-03-09_

叫用 Lync Server 2013 中央管理存放區的容錯移轉程序。當中央管理存放區執行容錯移轉時，會以預先指派的鏡像資料庫或指定的備份資料庫取代主要資料庫。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Invoke-CsManagementServerFailover -BackupSqlServerFqdn <Fqdn> -Force <SwitchParameter> [-BackupMirrorSqlInstanceName <String>] [-BackupMirrorSqlServerFqdn <Fqdn>] [-BackupSqlInstanceName <String>] <COMMON PARAMETERS>

    Invoke-CsManagementServerFailover [-Restore <SwitchParameter>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會為 Lync Server 2013容錯移轉中央管理存放區。此範例會以在 redmond-cs-001.litwareinc.com 電腦上找到的 RTC 資料庫執行個體取代現有的管理存放區。

    Invoke-CsManagementServerFailover -BackupSqlServerFqdn "redmond-cs-001.litwareinc.com" - BackupSqlInstanceName "RTC" -Force

## 詳細描述

**Invoke-CsManagementServerFailover** Cmdlet 可讓系統管理員容錯移轉中央管理伺服器 (CMS)。**Invoke-CsManagementServerFailover** Cmdlet 提供兩種方式來容錯移轉 CMS：1) 容錯移轉到指定的 SQL Server 執行個體，或 2) 容錯移轉到預先指派的鏡像資料庫。若要容錯移轉到指定的備份執行個體，請使用 BackupSqlServerFqdn 與 BackupSqlInstanceName 參數。若要容錯移轉到鏡像資料庫，請使用 BackupMirrorSqlServerFqdn 與 BackupMirrorSqlInstanceName 參數。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsManagementServerFailover"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Invoke-CsManagementServerFailover** Cmdlet 所執行的功能。

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
<td><p><em>BackupSqlServerFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>主控 SQL Server 備份資料庫之電腦的完整網域名稱。如果您是以災害復原模式來執行 <strong>Invoke-CsManagementServerFailover</strong> Cmdlet，此為必要參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。如果您是以災害復原模式來執行 <strong>Invoke-CsManagementServerFailover</strong> Cmdlet，此為必要參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>BackupMirrorSqlInstanceName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>鏡像資料庫的 SQL Server 執行個體。</p></td>
</tr>
<tr class="even">
<td><p><em>BackupMirrorSqlServerFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>主控 SQL Server 鏡像資料庫之電腦的完整網域名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>BackupSqlInstanceName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>備份資料庫的 SQL Server 執行個體。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\CMSFailover.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Restore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定此參數時，會還原現有的中央管理伺服器資料庫。</p></td>
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

無。**Invoke-CsManagementServerFailover** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Invoke-CsDatabaseFailover](invoke-csdatabasefailover.md)

