---
title: Uninstall-CsDatabase
TOCTitle: Uninstall-CsDatabase
ms:assetid: bd08ac1c-cfcd-4cf8-b082-7d2e83a2837e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412922(v=OCS.15)
ms:contentKeyID: 49292168
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Uninstall-CsDatabase

 

_**上次修改主題的時間：** 2015-03-09_

刪除指定的 Lync Server資料庫。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Uninstall-CsDatabase -DatabaseType <Application | Archiving | Monitoring | User | Provision | CentralAdmin | Lyss | Registrar | Edge | PersistentChat | PersistentChatCompliance | CentralMgmt> [-SqlInstanceName <String>] [-SqlServerFqdn <Fqdn>] <COMMON PARAMETERS>

    Uninstall-CsDatabase -CentralManagementDatabase <SwitchParameter> -SqlServerFqdn <Fqdn> [-SqlInstanceName <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Detach <SwitchParameter>] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會從電腦 atl-sql-001.litwareinc.com 刪除 中央管理存放區。

    Uninstall-CsDatabase -CentralManagementDatabase -SqlServerFqdn atl-sql-001.litwareinc.com 

## 範例 2

範例 2 會從電腦 atl-sql-001.litwareinc.com 刪除使用者資料庫。使用 DatabaseType 參數時，會刪除所有與指定資料庫相關的存放區。

    Uninstall-CsDatabase -DatabaseType User -SqlServerFqdn atl-sql-001.litwareinc.com 

## 詳細描述

Lync Server 會密集使用 SQL Server 資料庫 (如 中央管理存放區和 封存資料庫)。這些資料庫會在您安裝 Lync Server 的同時，或在您安裝需要資料庫後端之 Lync Server 角色的同時進行安裝。在安裝這些資料庫之後，您將很少需要解除安裝它們。

不過，您可能需要在某個時刻解除安裝 Lync Server 資料庫；例如，硬體故障或網路連線問題而使得現有資料庫無法使用。不管原因為何， **Uninstall-CsDatabase** Cmdlet 都提供一種方法，讓您移除 (或卸除) Lync Server 所使用的任何 SQL Server 資料庫。

誰可以執行這個 Cmdlet：您必須是網域的成員、SQL Server 系統管理員及已安裝 SQL Server 之電腦上的本機系統管理員，才能本機執行 **Uninstall-CsDatabase** Cmdlet。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Uninstall-CsDatabase"}

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
<td><p>如果 中央管理存放區 存在，則會解除安裝它。您無法在同一個命令中同時使用 CentralManagementDatabase 和 DatabaseType。</p></td>
</tr>
<tr class="even">
<td><p><em>DatabaseType</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.DatabaseNameType</p></td>
<td><p>要刪除的資料庫。有效值為：</p>
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
<p>User</p>
<p>若要刪除 中央管理存放區，請使用 CentralManagementDatabase 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>資料庫所在之電腦或 SQL Server 叢集的完整網域名稱 (FQDN)。例如：-SqlServer atl-sql-001.litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Detach</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>卸除指定的資料庫 (如其存在)。卸除資料庫時，會移除 SQL Server 加諸的所有檔案鎖定。這可讓您直接存取資料庫檔案，以便執行將那些檔案複製到其他電腦的這類動作。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>強制移除資料庫 (如其存在)，即使資料庫目前在使用中也是一樣。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\UninstallDatabase.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>包含要移除之資料庫的資料庫執行個體名稱。資料庫執行個體是一組提供資料庫檔案存取權的執行中程序。</p></td>
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

無。 **Uninstall-CsDatabase** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Uninstall-CsDatabase** Cmdlet 不會傳回任何值或物件。

## 請參閱

#### 其他資源

[Install-CsDatabase](install-csdatabase.md)

