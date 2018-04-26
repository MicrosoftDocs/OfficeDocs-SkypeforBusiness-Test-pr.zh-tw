---
title: Update-CsUserData
TOCTitle: Update-CsUserData
ms:assetid: e3cb48e9-9b5e-4c73-ab54-4aea16533ed8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205358(v=OCS.15)
ms:contentKeyID: 49292599
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsUserData

 

_**上次修改主題的時間：** 2015-03-09_

使用先前所匯出的使用者資訊更新 Lync Server 使用者資料。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Update-CsUserData -FileName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-RoutingGroupFilter <String>] [-UserFilter <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會根據儲存在檔案 C:\\Logs\\ExportedUserData.zip 中的資訊，來更新 Lync Server 使用者資料。

    Update-CsUserData -Filename "C:\Logs\ExportedUserData.zip"

## 範例 2

範例 2 會更新單一使用者的使用者資料：SIP 位址為 kenmyer@litwareinc.com 的使用者。作法是加入 UserFilter 參數加上使用者的 SIP 位址 (不包括 sip: 首碼)。

    Update-CsUserData -Filename "C:\Logs\ExportedUserData.zip" -UserFilter "kenmyer@litwareinc.com"

## 詳細描述

**Update-CsUserData** Cmdlet 可讓系統管理員更新指定使用者或使用者集合的使用者資料 (請注意，這些資料必須是使用 [Export-CsUserData](export-csuserdata.md) Cmdlet 匯出的資料)。通常需完成此更新，以便為登入的使用者還原遺失資料。

若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Update-CsUserData"}

**Lync Server 控制台:** The functions carried out by the **Update-CsUserData** cmdlet are not available in the Lync Server 控制台.

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
<td><p>含有要更新的使用者資料之 .ZIP 檔案或 .XML 檔案的完整路徑。例如：</p>
<p>-FileName &quot;C:\Data\Lync2010.zip&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>讓系統管理員指定執行 <strong>Update-CsUserData</strong> Cmdlet 時所使用之網域控制站的 FQDN。若未指定，該 Cmdlet 會使用第一個可用的網域控制站。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>RoutingGroupFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您只更新指定路由群組的資料。路由群組可用於指定要登錄使用者的前端伺服器。</p></td>
</tr>
<tr class="even">
<td><p><em>UserFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您更新單一使用者的資料。該使用者會使用其 SIP 位址 (不包括 sip: 首碼) 來指定。例如：</p>
<p>-UserFilter &quot;kenmyer@litwareinc.com&quot;</p></td>
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

無。 **Update-CsUserData** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Update-CsUserData** Cmdlet 會更新 Lync Server 使用者資訊。

## 請參閱

#### 其他資源

[Convert-CsUserData](convert-csuserdata.md)  
[Export-CsUserData](export-csuserdata.md)  
[Import-CsUserData](import-csuserdata.md)  
[Sync-CsUserData](sync-csuserdata.md)

