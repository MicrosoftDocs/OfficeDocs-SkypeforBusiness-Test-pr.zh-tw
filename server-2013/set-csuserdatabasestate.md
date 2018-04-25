---
title: Set-CsUserDatabaseState
TOCTitle: Set-CsUserDatabaseState
ms:assetid: c4d8fe5e-ebc1-443b-943d-fc54649e94fd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412973(v=OCS.15)
ms:contentKeyID: 49292243
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUserDatabaseState

 

_**上次修改主題的時間：** 2015-03-09_

啟用或停用一或多個 Lync Server 使用者資料庫。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsUserDatabaseState -RegistrarPool <Fqdn> <COMMON PARAMETERS>

    Set-CsUserDatabaseState -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -Online <$true | $false> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令可使 UserDatabase:atl-sql-001.litwareinc.com 使用者資料庫離線。只要將 Online 屬性設為 $False 即可。

    Set-CsUserDatabaseState -Identity "UserDatabase:atl-sql-001.litwareinc.com" -Online $False

## 範例 2

在範例 2 中，系統會使登錄器集區 atl-cs-001.litwareinc.com 中的所有使用者資料庫離線。

    Set-CsUserDatabaseState -RegistrarPool atl-cs-001.litwareinc.com -Online $False

## 範例 3

範例 3 會尋找所有目前為離線狀態的使用者資料庫，並使這些資料庫重新上線。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsUserDatabaseState** Cmdlet，以傳回組織中所有使用者資料庫的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Online 屬性等於 False 的資料庫。接著將篩選後的集合管線傳送到 **ForEach-Object** Cmdlet，以取得集合中的每一個資料庫，並將 Online 屬性設為 True。請注意，您必須將離線資料庫的集合管線傳送到 **ForEach-Object** Cmdlet 而非 **Set-CsUserDatabaseState** Cmdlet。這是因為後一個 Cmdlet 無法直接接受管線傳送的資訊。

    Get-CsUserDatabaseState | Where-Object {$_.Online -eq $False} | ForEach-Object {Set-CsUserDatabaseState -Identity $_.Identity -Online $True}

## 詳細描述

Lync Server 會利用使用者資料庫 (亦稱為使用者存放區) 來維護 Lync Server 使用者的狀態和路由資訊。**Set-CsUserDatabaseState** Cmdlet 可讓您變更一或多個使用者資料庫的狀態：只要利用 Cmdlet 使資料庫離線，或使停用的資料庫重新運作即可。

請注意，當您安裝 Lync Server 標準版時，預設不會啟用 SQL Server Express 的防火牆例外。這表示您無法從 Windows PowerShell 的遠端執行個體執行 **Set-CsUserDatabaseState** Cmdlet。這是因為命令將無法周遊防火牆和存取 SQL Server Express 資料庫。您仍然可以本機執行此 Cmdlet (亦即，在 Standard Edition Server 上)。但是，若要遠端執行 **Set-CsUserDatabaseState** Cmdlet，您需要針對 SQL Server Express 手動啟用防火牆例外。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsUserDatabaseState** Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUserDatabaseState"}

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
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要修改線上狀態之使用者資料庫的唯一識別碼。例如：-Identity &quot;UserDatabase:atl-sql-001.litwareinc.com&quot;。</p>
<p>您不能在同一個命令中同時使用 Identity 和 RegistrarPool，也不能將任一參數搭配萬用字元使用。</p></td>
</tr>
<tr class="even">
<td><p><em>Online</em></p></td>
<td><p>必要</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True ($True) 時，可使資料庫上線並可供使用。設為 False ($False) 時，可使資料庫離線。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPool</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>主控要修改線上狀態之使用者資料庫的登錄器集區完整網域名稱 (FQDN)。例如：-RegistrarPool atl-cs-001.litwareinc.com。</p>
<p>您不能在同一個命令中同時使用 –Identity 和 –RegistrarPool，也不能將任一參數搭配萬用字元使用。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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

字串。**Set-CsUserDatabaseState** Cmdlet 接受代表要更新之使用者資料庫 Identity 的字串值。

## 傳回類型

無。反之，**Set-CsUserDatabaseState** Cmdlet 會修改現有的 Microsoft.Rtc.Management.Xds.UserStoreState 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsUserDatabaseState](get-csuserdatabasestate.md)  
[Update-CsUserDatabase](update-csuserdatabase.md)

