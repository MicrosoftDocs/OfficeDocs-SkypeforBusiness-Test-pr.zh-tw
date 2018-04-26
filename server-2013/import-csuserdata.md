---
title: Import-CsUserData
TOCTitle: Import-CsUserData
ms:assetid: f39ef951-ee5b-4200-b6fb-68a4d4d6e86f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205373(v=OCS.15)
ms:contentKeyID: 49292800
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsUserData

 

_**上次修改主題的時間：** 2015-03-09_

匯入先前使用 Export-CsUserData Cmdlet 所匯出的使用者資料。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Import-CsUserData -PoolFqdn <Fqdn> <COMMON PARAMETERS>

    Import-CsUserData -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -FileName <String> [-ConfDirectoryFilter <String>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-LegacyFormat <SwitchParameter>] [-RoutingGroupFilter <String>] [-UserFilter <String>]

## 範例

## 範例 1

範例 1 所示的命令會將使用者資料從 C:\\Logs\\ExportedUserData.zip 檔案匯入集區 atl-cs-001.litwareinc.com。

    Import-CsUserData -PoolFqdn "atl-cs-001.litwareinc.com" -FileName "C:\Logs\ExportedUserData.zip"

## 詳細描述

Import-CsUserData Cmdlet 可用於將先前所儲存的使用者資料及/或會議目錄資料匯入 Lync Server。請注意，這些資料必須是 [Export-CsUserData](export-csuserdata.md) Cmdlet 匯出的資料。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsUserData"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Import-CsUserData** Cmdlet 所執行的功能。

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
<td><p><em>FileName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>含有已匯出使用者資料之輸入檔案的完整路徑。例如：</p>
<p>-InputFile &quot;C:\Data\ExportedUsers.xml&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要匯入資料之資料庫的服務識別。例如：</p>
<p>-Identity &quot;UserDatabase:atl-sql-001.litwareinc.com&quot;</p>
<p>請勿在同一個命令中同時使用 Identity 與 PoolFqdn 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>正在匯入使用者資料之登錄器集區的完整網域名稱。例如：</p>
<p>–PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>ConfDirectoryFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指定此參數時，可讓您匯入指定會議目錄的會議目錄資訊。例如，若要從識別碼為 13 的會議目錄匯入資料，請使用下列語法：</p>
<p>-ConfDirectoryFilter 13</p>
<p>您可以使用以下命令傳回會議目錄識別碼：</p>
<p>Get-CsConferenceDirectory</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>讓管理員指定要在執行 <strong>Import-CsUserData</strong> Cmdlet 時使用的網域控制站的 FQDN。若未指定，該 Cmdlet 會使用第一個可用的網域控制站。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>LegacyFormat</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指出要匯入的資料是從舊版 Lync Server 或 Office Communications Server 匯出。</p></td>
</tr>
<tr class="even">
<td><p><em>RoutingGroupFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您限制只可匯入相同路由群組之使用者的資料。Lync Server 會利用路由群組判別使用者登錄所在的前端伺服器。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您匯入單一使用者的使用者資料。若要轉換指定使用者的資料 (僅限該使用者)，請將 UserFilter 參數設為該使用者的 SIP 位址，並確定省略 sip: 首碼。例如：</p>
<p>-UserFilter &quot;kenmyer@litwareinc.com&quot;</p>
<p>此參數可讓您一次匯入一位使用者的資料。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Import-CsUserData** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Convert-CsUserData](convert-csuserdata.md)  
[Export-CsUserData](export-csuserdata.md)  
[Sync-CsUserData](sync-csuserdata.md)  
[Update-CsUserData](update-csuserdata.md)

