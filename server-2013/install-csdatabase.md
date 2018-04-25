---
title: Install-CsDatabase
TOCTitle: Install-CsDatabase
ms:assetid: e91c1800-35f6-40ef-840d-7a518bddcae6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399044(v=OCS.15)
ms:contentKeyID: 49292682
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Install-CsDatabase

 

_**上次修改主題的時間：** 2015-03-09_

安裝一或多個 Lync Server 資料庫。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Install-CsDatabase -LocalDatabases <SwitchParameter> [-ForDefaultInstance <SwitchParameter>] [-ForInstance <String>] <COMMON PARAMETERS>

    Install-CsDatabase -CentralManagementDatabase <SwitchParameter> -SqlServerFqdn <Fqdn> [-Backup <SwitchParameter>] [-Collocated <SwitchParameter>] [-SqlInstanceName <String>] <COMMON PARAMETERS>

    Install-CsDatabase -ConfiguredDatabases <SwitchParameter> -SqlServerFqdn <Fqdn> [-ExcludeCollocatedStores <SwitchParameter>] [-ForDefaultInstance <SwitchParameter>] [-ForInstance <String>] <COMMON PARAMETERS>

    Install-CsDatabase -DatabaseType <Application | Archiving | Monitoring | User | Provision | CentralAdmin | Lyss | Registrar | Edge | PersistentChat | PersistentChatCompliance | CentralMgmt> [-Collocated <SwitchParameter>] [-SqlInstanceName <String>] [-SqlServerFqdn <Fqdn>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Clean <SwitchParameter>] [-Confirm [<SwitchParameter>]] [-DatabasePathMap <Hashtable>] [-DatabasePaths <String[]>] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-NoReindex <SwitchParameter>] [-Report <String>] [-SkipPrepareCheck <SwitchParameter>] [-Update <SwitchParameter>] [-UseDefaultSqlPaths <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中， **Install-CsDatabase** Cmdlet 會讀取 Lync Server 拓撲，然後在集區 atl-sql-001.litwareinc.com 上安裝任何需要的資料庫。

    Install-CsDatabase -ConfiguredDatabases -SqlServerFqdn atl-sql-001.litwareinc.com -DatabasePaths "E:\CSLog","F:\CSLog","G:\CSDB"

## 範例 2

範例 2 所示的命令會在集區 atl-sql-001.litwareinc.com 上安裝 中央管理存放區。會將該資料庫安裝於 rtc 執行個體中，並使用資料夾 G:\\CSDB。

    Install-CsDatabase -CentralManagementDatabase -SqlServerFqdn atl-sql-001.litwareinc.com -SqlInstanceName rtc -DatabasePaths "G:\CSDB"

## 詳細描述

Lync Server 會密集使用 SQL Server 資料庫，範圍從 中央管理存放區 至 封存資料庫。依照通則，在您安裝 Lync Server 或安裝需要資料庫後端的 Lync Server 角色時 (例如 監控伺服器)，同時也會設定這些資料庫。安裝後，通常不需重新安裝這些資料庫，或將資料庫移往新的位置。

不過，在少數情況下，您可能需要以手動方式安裝 Lync Server 資料庫；這可能是因為您需要將資料庫移至另一個伺服器，或因為與設定相關的問題所以無法為您安裝資料庫。 **Install-CsDatabase** Cmdlet 會提供您安裝 Lync Server 所使用之任何 SQL Server 資料庫的方法。

執行 **Install-CsDatabase** Cmdlet 時，基本上有三個方法可以處理要安裝的資料庫組態：

選項 1 -- 執行不含指定資料庫路徑之參數的 Cmdlet。執行不含 DatabasePath 或 UseDefaultSqlPath 參數的 **Install-CsDatabase** Cmdlet 時，Cmdlet 會使用內建的演算法，來選擇資料庫記錄及資料檔案的儲存位置。請注意，這個內建的演算法會與獨立的 SQL Server 共同運作，但無法與 SQL Server 叢集共同運作。您的命令必須加入 DatabasePath 或 UseDefaultSqlPathtall 參數，才能在 SQL Server 叢集上安裝資料庫。

選項 2 -- 執行 Cmdlet 搭配 DatabasePath 參數。執行 **Install-CsDatabase** Cmdlet 搭配 DatabasePath 參數時，系統不會使用內建的演算法來選擇資料庫記錄及資料檔案的儲存位置。而是由系統管理員選取這些記錄及資料檔案的位置。只要指定應儲存此資料的資料夾路徑，即可在相同位置安裝資料檔案及 SQL Server 記錄。例如：

\-DatabasePath C:\\SqlData

如果要將資料檔案及記錄檔案儲存在第二個位置，請指定每個資料夾的路徑，並使用逗號分隔兩個位置 (請注意，不要在逗號前後留空格)：

\-DatabasePath C:\\SqlLogs,D:\\SqlData

記錄檔案會永遠儲存在第一個指定的位置，而資料檔案則會儲存在第二個位置。

在集區後端中，特定記錄檔案可能會自行儲存在磁碟機上。如果您在單一磁碟機有集區後端，檔案會以下列方式分佈：

磁碟機 1 – Rtcdyn 記錄、Rtc 記錄、其他記錄、其他資料。

如果您有兩個磁碟機，檔案會以下列方式分佈：

磁碟機 1 – Rtcdyn 記錄、Rtc 記錄。

磁碟機 2 – 其他記錄、其他資料。

有三個磁碟機：

磁碟機 1 – Rtcdyn 記錄。

磁碟機 2 – Rtc 記錄。

磁碟機 3 – 其他記錄、其他資料。

有四個磁碟機：

磁碟機 1 – Rtcdyn 記錄。

磁碟機 2 – Rtc 記錄。

磁碟機 3 – 其他記錄。

磁碟機 4 – 其他資料。

選項 3 -- 執行 Cmdlet 搭配 UseDefaultSqlPaths 參數。執行 **Install-CsDatabase** Cmdlet 搭配 UseDefaultSqlPaths 參數時，系統不會使用內建的演算法來選擇資料庫記錄及資料檔案的儲存位置。而是將記錄及資料檔案儲存在 SQL Server 預設路徑 (這些路徑必須由 SQL Server 系統管理員事先設定) 指定的位置中。資料檔案會儲存在預設的 SQL Server 資料檔案位置中，而記錄檔案則儲存在預設的 SQL Server 記錄檔案位置中。

執行 **Install-CsDatabase** Cmdlet 前，請務必確認未將 RTCUniversalServerAdmins 群組指派為資料庫擁有者。如果將該群組列為擁有者，當您呼叫 **Install-CsDatabase** Cmdlet 時，該群組可能會遭刪除。

誰可以執行此 Cmdlet：您必須是網域的成員、RTCUniversalReadOnlyAdmins 群組的成員、SQL Server 系統管理員及已安裝 SQL Server 之電腦上的本機系統管理員，才能在本機執行 **Install-CsDatabase** Cmdlet。若要傳回已指派此 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自行建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Install-CsDatabase"}

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
<td><p>如果加入此參數， <strong>Install-CsDatabase</strong> Cmdlet 會使用 SqlServerFqdn 參數，在指定的電腦上安裝 中央管理存放區。通常只有 拓撲產生器會使用此參數，且一般只在初始安裝時呼叫一次。</p></td>
</tr>
<tr class="even">
<td><p><em>ConfiguredDatabases</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 Lync Server 拓撲讀取資訊，並在指定的 SQL Server 電腦或 SQL Server 叢集上安裝所需的資料庫。需要呼叫 <strong>Install-CsDatabase</strong> Cmdlet 的系統管理員在指定要安裝的資料庫時，幾乎一律會使用此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>DatabaseType</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.DatabaseNameType</p></td>
<td><p>可讓您在特定 SQL Server 電腦或 SQL Server 叢集上安裝特定的資料庫。除非由 Microsoft 支援人員指示，否則一般來說，系統管理員不應執行 <strong>Install-CsDatabase</strong> Cmdlet 搭配 DatabaseType 參數。系統管理員通常應改用 ConfiguredDatabases 參數。DatabaseType 參數會要求您瞭解拓撲中所用每個資料庫的確切類型與位置，且僅在 <strong>Install-CsDatabase</strong> Cmdlet 命令使用 ConfiguredDatabases 參數執行失敗時才需要使用。</p>
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
<td><p><em>LocalDatabases</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果加入此參數， <strong>Install-CsDatabase</strong> Cmdlet 將會讀取 Lync Server 拓撲並安裝資料庫，同時視需要儲存於本機電腦上。</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>要安裝資料庫之電腦的完整網域名稱 (FQDN)。例如：-SqlServerFqdn atl-sql-001.litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>Backup</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>使用時，會將現有的中央管理伺服器資料庫備份至指定的 SQL Server 執行個體。</p></td>
</tr>
<tr class="odd">
<td><p><em>Clean</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果加入此參數， <strong>Install-CsDatabase</strong> Cmdlet 將會視需要刪除並重新安裝資料庫。如果未加入此參數， <strong>Install-CsDatabase</strong> Cmdlet 將不會覆寫任何現有的資料庫。您無法在同一個命令中同時使用 Clean 與 Update。</p></td>
</tr>
<tr class="even">
<td><p><em>Collocated</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>若使用，將會與中央管理存放區一起收集其他的資料庫角色。</p></td>
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
<td><p><em>DatabasePaths</em></p></td>
<td><p>選用</p></td>
<td><p>System.String[]</p></td>
<td><p>指定可以儲存資料與記錄檔案的磁碟機與資料夾，例如：-DatabasePaths &quot;D:\Logs&quot;,&quot;E:\Data&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeCollocatedStores</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>使用時，隱藏告訴您任何配置的資料庫存放區必須安裝在本機電腦上的警告訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>使用時，即使該類型的現有資料庫目前正在使用中，也會強制執行新資料庫的安裝。</p></td>
</tr>
<tr class="even">
<td><p><em>ForDefaultInstance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果指定此參數，請指示 <strong>Install-CsDatabase</strong> Cmdlet 僅對預設的 SQL Server 執行個體採取動作。您無法在同一個命令中同時使用 ForDefaultInstance 和 ForInstance。</p></td>
</tr>
<tr class="odd">
<td><p><em>ForInstance</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>如果指定此參數，請指示 <strong>Install-CsDatabase</strong> Cmdlet 僅對指定的 SQL Server 執行個體採取動作。您無法在同一個命令中同時使用 ForInstance 和 ForDefaultInstance。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中通用類別目錄伺服器的完整網域名稱 (FQDN)。如果您執行 <strong>Install-CsDatabase</strong> Cmdlet 的電腦帳戶是在您的網域中，就不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>儲存全域設定之網域控制器的完整網域名稱 (FQDN)。如果全域設定是儲存在 Active Directory 網域服務 的系統容器內，則此參數必須導向根網域控制器。如果全域設定儲存在組態容器中，則會使用任何一個網域控制站，且會省略此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>NoReindex</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>防止在更新資料庫時重新建立索引檔案。此參數只能搭配 Update 參數使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\InstallDatabases.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SkipPrepareCheck</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果使用此參數，會造成 <strong>Install-CsDatabase</strong> Cmdlet 放棄初始準備檢查。</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要安裝資料庫之資料庫執行個體的名稱。資料庫執行個體只是一組提供資料庫檔案存取的執行程序。如果省略此參數， <strong>Install-CsDatabase</strong> Cmdlet 將會使用預設的 SQL Server 執行個體。</p></td>
</tr>
<tr class="even">
<td><p><em>Update</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>使用時，會更新現有的資料庫。您無法在同一個命令中同時使用 Update 與 Clean。</p>
<p>請注意，Update 參數不適用於鏡像資料庫。鏡像資料庫因為無法刪除或重新建立，所以會導致此命令失敗。若要對鏡像資料庫使用 Update 參數，必須先使用 <a href="uninstall-csmirrordatabase.md">Uninstall-CsMirrorDatabase</a> Cmdlet 解除鏡像伺服器的關聯，然後再搭配執行 Install-CsDatabase 與 Update 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>UseDefaultSqlPaths</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定時，請指示 SQL Server 選取要儲存資料及記錄檔案的磁碟機。</p></td>
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

無。 **Install-CsDatabase** Cmdlet 不接受以管線傳送的輸入。

## 傳回類型

**Install-CsDatabase** Cmdlet 不會傳回任何值或物件。

## 請參閱

#### 其他資源

[Uninstall-CsDatabase](uninstall-csdatabase.md)

