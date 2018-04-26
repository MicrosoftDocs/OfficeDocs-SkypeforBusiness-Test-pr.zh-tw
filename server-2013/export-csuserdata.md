---
title: Export-CsUserData
TOCTitle: Export-CsUserData
ms:assetid: 52c411e1-76da-48b8-b1e3-ddc7c7f86e3d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204897(v=OCS.15)
ms:contentKeyID: 49290921
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsUserData

 

_**上次修改主題的時間：** 2015-03-09_

以能夠匯入 Lync Server 的格式匯出使用者資料。資料將會以包含成對之 XML 文件的 .ZIP 檔案形式匯出。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Export-CsUserData -PoolFqdn <Fqdn> <COMMON PARAMETERS>

    Export-CsUserData -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -FileName <String> [-ConfDirectoryFilter <String>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-LegacyFormat <SwitchParameter>] [-UserFilter <String>]

## 範例

## 範例 1

範例 1 所示的命令會將使用者資料從 atl-cs-001.litwareinc.com 集區匯出至名為 C:\\Logs\\ExportedUserData.zip 的檔案。

    Export-CsUserData -PoolFqdn "atl-cs-001.litwareinc.com" -FileName "C:\Logs\ExportedUserData.zip"

## 詳細描述

**Export-CsUserData** Cmdlet 可讓系統管理員匯出 Lync Server 集區的使用者資料與/或會議目錄。這些資料可以 Lync Server 2013 或 Microsoft Lync Server 2010 所用的使用者資料格式儲存，然後再透過 [Import-CsUserData](import-csuserdata.md) Cmdlet 匯入。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsUserData"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Export-CsUserData** Cmdlet 所執行的功能。

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
<td><p>System.Strkng</p></td>
<td><p><strong>Export-CsUserData</strong> Cmdlet 將要建立之 .ZIP 檔的完整路徑；此檔案將會包含匯出的使用者資料。例如：</p>
<p>-FileName &quot;C:\Logs\ExportedData.zip&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>要匯出之使用者資料所在資料庫安裝所在集區的完整網域名稱。例如：</p>
<p>-Identity &quot;atl-sql-001.litwareinc.com&quot;</p>
<p>請注意，您可以執行下列命令來擷取使用者資料庫集區的完整網域名稱：</p>
<p>Get-CsService –UserDatabase</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>要匯出之使用者資料所在登錄器集區的完整網域名稱。例如：</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>ConfDirectoryFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>指定此參數時，可讓您針對指定的會議目錄，匯出會議目錄資訊。例如，若要從識別碼為 13 的會議目錄匯出資料，請使用下列語法：</p>
<p>-ConfDirectoryFilter 13</p>
<p>您可以使用下列命令傳回會議目錄 ID：</p>
<p>Get-CsConferenceDirectory</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>讓系統管理員指定執行 <strong>Export-CsUserData</strong> Cmdlet 時所使用之網域控制站的 FQDN。若未指定，該 Cmdlet 會使用第一個可用的網域控制站。</p></td>
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
<td><p>如有指定，資料會以 Microsoft Lync Server 2010 所使用的格式儲存。</p></td>
</tr>
<tr class="even">
<td><p><em>UserFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓您為單一使用者匯出資料。若要指定該使用者，您可以指定其 SIP 位址，並去掉 sip: 首碼。例如：</p>
<p>-UserFilter &quot;kenmyer@litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Export-CsUserData** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Export-CsUserData** Cmdlet 會建立新的 .ZIP 檔案。

## 請參閱

#### 其他資源

[Convert-CsUserData](convert-csuserdata.md)  
[Import-CsUserData](import-csuserdata.md)  
[Sync-CsUserData](sync-csuserdata.md)  
[Update-CsUserData](update-csuserdata.md)

