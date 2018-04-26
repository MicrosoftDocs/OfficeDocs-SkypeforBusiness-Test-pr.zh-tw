---
title: Get-CsUserDatabaseState
TOCTitle: Get-CsUserDatabaseState
ms:assetid: c90150cd-fdb0-4c79-af58-c9ad884cb043
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398831(v=OCS.15)
ms:contentKeyID: 49292291
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUserDatabaseState

 

_**上次修改主題的時間：** 2015-03-09_

傳回一或多個 Lync Server 使用者資料庫之線上狀態的資訊 (True 或 False)。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsUserDatabaseState [-RegistrarPool <Fqdn>] <COMMON PARAMETERS>

    Get-CsUserDatabaseState [-Identity <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之各個使用者資料庫的線上狀態。

    Get-CsUserDatabaseState

## 範例 2

範例 2 所示的命令會傳回單一使用者資料庫的線上狀態：Identity 為 UserDatabase:atl-sql-001.litwareinc.com 的資料庫。

    Get-CsUserDatabaseState -Identity "UserDatabase:atl-sql-001.litwareinc.com"

## 範例 3

在範例 3 中，此命令會傳回登錄器集區 atl-cs-001.litwareinc.com 中所有使用者資料庫的狀態資訊。

    Get-CsUserDatabaseState -RegistrarPool "atl-cs-001.litwareinc.com"\

## 範例 4

範例 4 會傳回所有目前為線上狀態之使用者資料庫的資訊。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsUserDatabaseState** Cmdlet，以傳回組織使用之所有使用者資料庫的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Online 屬性等於 True 的資料庫。

    Get-CsUserDatabaseState | Where-Object {$_.Online -eq $True}

## 詳細描述

Lync Server 會利用使用者資料庫 (亦稱為使用者存放區) 來維護 Lync Server 使用者的狀態和路由資訊。**Get-CsUserDatabaseState** Cmdlet 可讓您驗證組織中所有目前使用之使用者資料庫的現行狀態 (線上或離線)。

請注意，當您安裝 Lync Server 標準版時，預設不會啟用 SQL Server Express 的防火牆例外。這表示您無法從 Windows PowerShell 的遠端執行個體執行 **Get-CsUserDatabaseState** Cmdlet。這是因為命令將無法周遊防火牆和存取 SQL Server Express 資料庫。您仍然可以本機執行此 Cmdlet (亦即，在 Standard Edition Server 上)。但是，若要遠端執行 **Get-CsUserDatabaseState** Cmdlet，您需要針對 SQL Server Express 手動啟用防火牆例外。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsUserDatabaseState** Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUserDatabaseState"}

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
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要傳回線上狀態之使用者資料庫的唯一識別碼。例如：-Identity &quot;UserDatabase:atl-sql-001.litwareinc.com&quot;。</p>
<p>您不能在同一個命令中同時使用 Identity 和 RegistrarPool，也不能將這任一個參數搭配萬用字元使用。如果同時省略這兩個參數，<strong>Get-CsUserDatabaseState</strong> Cmdlet 會傳回所有目前正在使用之使用者資料庫的資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPool</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>主控要傳回線上狀態之使用者資料庫的登錄器集區完整網域名稱。例如：-RegistrarPool &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p>您不能在同一個命令中同時使用 Identity 和 RegistrarPool，也不能將這任一個參數搭配萬用字元使用。如果同時省略這兩個參數，<strong>Get-CsUserDatabaseState</strong> Cmdlet 會傳回所有目前正在使用之使用者資料庫的資訊。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsUserDatabaseState** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsUserDatabaseState** Cmdlet 會傳回 Microsoft.Rtc.Management.Xds.UserStoreState 物件的執行個體。

## 請參閱

#### 其他資源

[Set-CsUserDatabaseState](set-csuserdatabasestate.md)  
[Update-CsUserDatabase](update-csuserdatabase.md)

