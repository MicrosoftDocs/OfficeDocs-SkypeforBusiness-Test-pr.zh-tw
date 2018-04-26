---
title: Uninstall-CsMirrorDatabase
TOCTitle: Uninstall-CsMirrorDatabase
ms:assetid: a5b14259-6cf6-46b5-ae8d-3b5e4428dfaf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205159(v=OCS.15)
ms:contentKeyID: 49291898
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Uninstall-CsMirrorDatabase

 

_**上次修改主題的時間：** 2015-03-09_

解除安裝 Lync Server 2013 管理命令介面鏡像資料庫。資料庫鏡像可讓您同時維護兩個資料庫，而兩個資料庫各在不同的伺服器上。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Uninstall-CsMirrorDatabase -DatabaseType <Application | Archiving | Monitoring | User | Provision | CentralAdmin | Lyss | Registrar | Edge | PersistentChat | PersistentChatCompliance | CentralMgmt> -SqlServerFqdn <Fqdn> [-SqlInstanceName <String>] [-Confirm [<SwitchParameter>]] [-DropExistingDatabasesOnMirror <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會從電腦 atl-mirror-001.litwareinc.com 上的 SQL Server 執行個體 RTC 解除安裝使用者資料庫。由於已加入 DropExistingDatabaseOnMirror 參數，因此命令也會刪除實際的使用者資料庫鏡像。

    Uninstall-CsMirrorDatabase -SqlServerFqdn "atl-mirror-001.litwareinc.com" -SqlInstanceName "RTC" -DatabaseType "User" -DropExistingDatabasesOnMirror

## 詳細描述

鏡像資料庫可讓您同時維護兩個資料庫。當資料寫入資料庫 A 時，該資料也會寫入其鏡像資料庫。這樣便能在資料庫 A 無法使用時立即取代該資料庫：您可以「容錯移轉」到鏡像資料庫，縮短使用者中斷使用的時間，以及降低資料損失。

您可以使用 [Install-CsMirrorDatabase](install-csmirrordatabase.md) Cmdlet 安裝並設定鏡像資料庫。如需移除鏡像資料庫，可以使用 **Uninstall-CsMirrorDatabase** Cmdlet。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Uninstall-CsMirrorDatabase"}

Lync Server 控制台：Lync Server 控制台不提供 **Uninstall-CsMirrorDatabase** Cmdlet 所執行的功能。

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
<tr class="even">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>要解除安裝之資料庫所在電腦的完整網域名稱 (FQDN)。例如：</p>
<p>-SqlServerFqdn atl-sql-001.litwareinc.com</p>
<p>這應為主要 SQL 伺服器電腦的 FQDN。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DropExistingDatabasesOnMirror</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會從鏡像伺服器刪除任何現有的鏡像資料庫複本。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-</p>
<p>Report &quot;C:\Logs\UnInstallDatabaseMirror.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要安裝資料庫之資料庫執行個體的名稱。資料庫執行個體只是一組提供資料庫檔案存取的執行程序。如果省略此參數，<strong>Uninstall-CsMirrorDatabase</strong> Cmdlet 將會使用預設的 SQL Server 執行個體。</p></td>
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

無。**Uninstall-CsMirrorDatabase** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Get-CsDatabaseMirrorState](get-csdatabasemirrorstate.md)  
[Install-CsMirrorDatabase](install-csmirrordatabase.md)

