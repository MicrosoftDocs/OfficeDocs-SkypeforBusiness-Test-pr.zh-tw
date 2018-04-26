---
title: Invoke-CsDatabaseFailover
TOCTitle: Invoke-CsDatabaseFailover
ms:assetid: 24b73e8e-948c-4e9c-bf4e-04ec0a229ffa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204744(v=OCS.15)
ms:contentKeyID: 49290360
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsDatabaseFailover

 

_**上次修改主題的時間：** 2015-03-09_

叫用 Lync Server 2013資料庫容錯移轉至其鏡像資料庫的程序。容錯移轉完成之後，鏡像資料庫會變成處理所有新資料庫要求的主要資料庫。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Invoke-CsDatabaseFailover -DatabaseType <Application | Archiving | Monitoring | User | Provision | CentralAdmin | Lyss | Registrar | Edge | PersistentChat | PersistentChatCompliance | CentralMgmt> -NewPrincipal <Primary | Mirror> -PoolFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-ExcludeDatabaseList <String[]>] [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會針對在 atl-cs-001.litwareinc.com 集區上找到的使用者資料庫叫用容錯移轉。此命令會導致使用者資料庫容錯移轉至先前指派的鏡像資料庫。

    Invoke-CsDatabaseFailover -PoolFqdn atl-cs-001.litwareinc.com -DatabaseType "User" -NewPrincipal "Mirror"

## 範例 2

在範例 2 中，除了 LcsCDR 與 LcsLog 資料庫之外，集區 atl-cs-001.litwareinc.com 上的所有資料庫皆會予以容錯移轉。您可以使用 ExcludeDatabaseList 參數指定不要容錯移轉的資料庫。

    Invoke-CsDatabaseFailover -PoolFqdn atl-cs-001.litwareinc.com -ExcludeDatabase -NewPrincipal "Mirror" -ExcludeDatabaseList "LcsCDR", "LcsLog"

## 詳細描述

**Invoke-CsDatabaseFailover** Cmdlet 可讓系統管理員容錯移轉一或多個 Lync Server 2013 資料庫。假設您需要暫時關閉主要資料庫，以便於進行硬體升級。此時就可以使用 **Invoke-CsDatabaseFailover** Cmdlet 將主要資料庫容錯移轉到鏡像資料庫。在執行此作業時，所有有問題之資料庫的要求皆會路由到鏡像資料庫。之後當硬體升級完成之後，可以再使用此 Cmdlet 容錯移轉回主要資料庫。

請注意，有問題的資料庫若未設定主要資料庫與鏡像資料庫，將會導致所有使用 **Invoke-CsDatabaseFailover** Cmdlet 的命令皆會失敗。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsDatabaseFailover"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Invoke-CsDatabaseFailover** Cmdlet 所執行的功能。

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
<td><p>要容錯移轉之資料庫的類型。有效值為：</p>
<p>Application</p>
<p>Archiving</p>
<p>CentralAdmin</p>
<p>CentralMgmt</p>
<p>Cls</p>
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
<td><p><em>NewPrincipal</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.MirrorRole</p></td>
<td><p>指定容錯移轉的對象是主要資料庫或鏡像資料庫。有效值為：</p>
<p>Mirror</p>
<p>Primary</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>包含要容錯移轉資料庫之集區的完整網域名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludeDatabaseList</em></p></td>
<td><p>選用</p></td>
<td><p>System.String[]</p></td>
<td><p>不應容錯移轉的資料庫清單。例如：</p>
<p>-ExcludeDatabaseList &quot;LcsCDR&quot;</p>
<p>若要防止多個資料庫容錯移轉，請使用逗號將資料庫名稱隔開：</p>
<p>-ExcludeDatabaseList &quot;LcsCDR&quot;, &quot;LcsLog&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取拓撲資訊，而不從中央管理存放區本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\DatabaseFailover.html&quot;</p></td>
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

無。**Invoke-CsDatabaseFailover** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Get-CsDatabaseMirrorState](get-csdatabasemirrorstate.md)  
[Install-CsMirrorDatabase](install-csmirrordatabase.md)

