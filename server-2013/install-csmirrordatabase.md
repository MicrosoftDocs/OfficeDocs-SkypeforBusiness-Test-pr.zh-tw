---
title: Install-CsMirrorDatabase
TOCTitle: Install-CsMirrorDatabase
ms:assetid: 6e3acdfb-39da-4aa4-b125-1ea542971da3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204986(v=OCS.15)
ms:contentKeyID: 49291241
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Install-CsMirrorDatabase

 

_**上次修改主題的時間：** 2015-03-09_

關聯鏡像資料庫與 Lync Server 2013 資料庫。資料庫鏡像可讓您同時維護資料庫的兩個複本，且兩個複本各位在不同的伺服器上。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Install-CsMirrorDatabase -ConfiguredDatabases <SwitchParameter> -SqlServerFqdn <Fqdn> [-ForDefaultInstance <SwitchParameter>] [-ForInstance <String>] <COMMON PARAMETERS>

    Install-CsMirrorDatabase -DatabaseType <Application | Archiving | Monitoring | User | Provision | CentralAdmin | Lyss | Registrar | Edge | PersistentChat | PersistentChatCompliance | CentralMgmt> -SqlServerFqdn <Fqdn> [-SqlInstanceName <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -FileShare <String> [-Confirm [<SwitchParameter>]] [-DatabasePathMap <Hashtable>] [-DropExistingDatabasesOnMirror <SwitchParameter>] [-ExcludeDatabaseList <String[]>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會安裝任何預先定義的資料庫。ConfiguredDatabases 參數會使 **Install-CsMirrorDatabase** Cmdlet 使用目前的拓撲來決定應為哪些資料庫。

    Install-CsMirrorDatabase -ConfiguredDatabases -FileShare "\\atl-fs-001\DbBackup" -SqlServerFqdn "atl-primary-001.litwareinc.com" -DropExisitingDatabasesOnMirror

## 詳細描述

鏡像資料庫可讓您同時維護資料庫的兩個複本。當資料寫入資料庫 A 時，該資料也會寫入其鏡像資料庫。如此一來，當資料庫 A 無法使用時，您可以利用容錯移轉功能，立即以鏡像資料庫取代資料庫 A，不僅可以將使用者中斷使用的時間縮短，也可將資料遺失降至最低。您可以在安裝主要資料庫之後，使用 **Install-CsMirrorDatabase** Cmdlet 安裝及設定鏡像資料庫。

**Install-CsMirrorDatabase** Cmdlet 預設會為所有位在指定伺服器上的 Lync Server 資料庫安裝及設定鏡像資料庫。但您可以使用 DatabaseType 或 ExcludeDatabaseList 參數，明確指定要安裝及不安裝的鏡像資料庫。DatabaseType 可讓您指定要安裝的資料庫，而 ExcludeDatabaseList 則可讓您指定不要安裝的資料庫。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Install-CsMirrorDatabase"}

Lync Server 控制台：Lync Server 控制台不提供 **Install-CsMirrorDatabase** Cmdlet 所執行的功能。

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
<td><p><em>ConfiguredDatabases</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 Lync Server 拓撲讀取資訊，並在指定的 SQL Server 電腦上或 SQL Server 叢集上安裝所需的鏡像資料庫。</p></td>
</tr>
<tr class="even">
<td><p><em>DatabaseType</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.DatabaseNameType</p></td>
<td><p>要安裝的鏡像資料庫類型。允許的值為：</p>
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
<tr class="odd">
<td><p><em>FileShare</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>資料庫共用資料夾的 UNC 路徑。檔案共用用於匯出主要 SQL Server 的資料庫並匯入至鏡像中。</p>
<p>共用資料夾與其內容可於鏡像建立後刪除。若您決定要停用鏡像，亦應刪除此資料夾。</p></td>
</tr>
<tr class="even">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>主要 SQL Server 電腦的完整網域名稱 (FQDN)。例如：</p>
<p>-SqlServerFqdn atl-sql-001.litwareinc.com</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DatabasePathMap</em></p></td>
<td><p>選用</p></td>
<td><p>System.Collections.Hashtable</p></td>
<td><p>可讓您指定資料檔案和記錄檔的自訂資料夾路徑；多個路徑應該以分號 (;) 分隔。例如：</p>
<p>-DatabasePathMap @{&quot;Archiving:DbPath&quot;=&quot;\\atl-sql-001.litwareinc.com\db&quot;;&quot;Archiving:LogPath&quot;=&quot;\\atl-sql-002.litwareinc.com\logs&quot;}</p></td>
</tr>
<tr class="odd">
<td><p><em>DropExistingDatabasesOnMirror</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會先從做為鏡像的伺服器刪除鏡像資料庫的任何現有複本，然後才會將新資料複製到該伺服器。</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeDatabaseList</em></p></td>
<td><p>選用</p></td>
<td><p>System.String[]</p></td>
<td><p>不應包含在鏡像資料庫中的資料庫清單；若要指定多個資料庫，可使用逗號將那些資料庫隔開。例如：</p>
<p>-ExcludeDatabaseList &quot;RTCCAB&quot;,&quot;RTCPROV&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ForDefaultInstance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果指定此參數，請指示 <strong>Install-CsMirrorDatabase</strong> Cmdlet 僅對預設的 SQL Server 執行個體採取動作。您無法在同一個命令中同時使用 ForDefaultInstance 和 ForInstance。</p></td>
</tr>
<tr class="even">
<td><p><em>ForInstance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>如果指定此參數，請指示 <strong>Install-CsMirrorDatabase</strong> Cmdlet 僅對指定的 SQL Server 執行個體採取動作。您無法在同一個命令中同時使用 ForInstance 和 ForDefaultInstance。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-</p>
<p>Report &quot;C:\Logs\InstallDatabaseMirror.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要安裝資料庫之資料庫執行個體的名稱。資料庫執行個體只是一組提供資料庫檔案存取的執行程序。如果省略此參數，<strong>Install-CsMirrorDatabase</strong> Cmdlet 將會使用預設的 SQL Server 執行個體。</p></td>
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

無。**Install-CsMirrorDatabase** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Get-CsDatabaseMirrorState](get-csdatabasemirrorstate.md)  
[Uninstall-CsMirrorDatabase](uninstall-csmirrordatabase.md)

