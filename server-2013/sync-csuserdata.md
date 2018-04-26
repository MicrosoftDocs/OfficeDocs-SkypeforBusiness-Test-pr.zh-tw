---
title: Sync-CsUserData
TOCTitle: Sync-CsUserData
ms:assetid: c385041f-f3f7-4db0-9ca7-b5f20a5d81d5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205242(v=OCS.15)
ms:contentKeyID: 49292227
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Sync-CsUserData

 

_**上次修改主題的時間：** 2015-03-09_

同步 Lync Server 2013 集區配對的使用者資料。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Sync-CsUserData -PoolFqdn <Fqdn> [-LocalStore <SwitchParameter>] [-RoutingGroup <String>] [-Target <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會同步集區 atl-cs-001.litwareinc.com 及其指定備份集區。

    Sync-CsUserData -PoolFqdn "atl-cs-001.litwareinc.com"

## 詳細描述

**Sync-CsUserData** Cmdlet 可同步登錄器集區及其指派備份集區間的使用者資料。請注意，如果有問題的集區尚未啟動備份服務，所有對此 Cmdlet 的呼叫都會失敗。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Sync-CsUserData"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Sync-CsUserData** Cmdlet 所執行的功能。

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
<td><p><em>PoolFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>主要 Lync Server 2013集區的完整網域名稱。例如：</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取使用者資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
<tr class="odd">
<td><p><em>RoutingGroup</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您只同步指定路由群組的資料。路由群組可用於指定要登錄使用者的前端伺服器。</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>與預先指定的備份集區同步資料。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Sync-CsUserData** Cmdlet 不接受管線傳送的輸出。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Convert-CsUserData](convert-csuserdata.md)  
[Export-CsUserData](export-csuserdata.md)  
[Import-CsUserData](import-csuserdata.md)  
[Update-CsUserData](update-csuserdata.md)

