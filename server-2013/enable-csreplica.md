---
title: Enable-CsReplica
TOCTitle: Enable-CsReplica
ms:assetid: 4a745da5-5b09-4b5a-8ab6-8b8b03d7afc6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425965(v=OCS.15)
ms:contentKeyID: 49290833
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsReplica

 

_**上次修改主題的時間：** 2015-03-09_

將本機電腦新增到 Lync Server 複寫路徑。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Enable-CsReplica [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將本機電腦新增至 Lync Server 複寫路徑。

    Enable-CsReplica

## 詳細描述

在電腦上安裝某項服務或伺服器角色時，必須將該電腦新增至複寫路徑；如此可讓該電腦從 中央管理存放區 接收拓撲和組態檔。**Enable-CsReplica** Cmdlet 可讓您手動將電腦新增至複寫路徑。您通常不需要手動將電腦新增至複寫路徑。而是系統會在您於電腦上安裝 Lync Server 時自動這樣進行。

誰可以執行這個 Cmdlet：您必須是本機系統管理員或網域的成員，才能在本機執行 **Enable-CsReplica** Cmdlet。

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中通用類別目錄伺服器的完整網域名稱 (FQDN)。如果您要在電腦上使用網域中的帳戶執行 <strong>Enable-CsReplica</strong> Cmdlet，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>儲存全域設定之網域控制站的 FQDN。如果全域設定是儲存在 Active Directory 網域服務 的系統容器內，則此參數必須導向根網域控制器。如果全域設定儲存在組態容器中，則會使用任何一個網域控制站，且會省略此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\EnableReplica.html&quot;</p></td>
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

無。**Enable-CsReplica** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。**Enable-CsReplica** Cmdlet 不會傳回任何值或物件。

## 請參閱

#### 其他資源

[Get-CsManagementStoreReplicationStatus](get-csmanagementstorereplicationstatus.md)

