---
title: Get-CsPoolBackupRelationship
TOCTitle: Get-CsPoolBackupRelationship
ms:assetid: 230bbb04-b4cb-410f-8284-00740558655d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204745(v=OCS.15)
ms:contentKeyID: 49290344
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPoolBackupRelationship

 

_**上次修改主題的時間：** 2015-03-09_

傳回與 商務用 Skype Online 集區相關聯之備份集區的資訊。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsPoolBackupRelationship -PoolFqdn <Fqdn> [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回指派給 atl-cs-001.litwareinc.com 集區之備份關係的資訊。

    Get-CsPoolBackupRelationship -PoolFqdn "atl-cs-001.litwareinc.com"

## 詳細描述

G**et-CsPoolBackupRelationship** Cmdlet 會傳回登錄器集區所關聯之備份集區的完整網域名稱。請注意，此為唯讀資訊，因此不會有對應的 **Set-CsPoolBackupRelationship** Cmdlet 可以讓您使用 Windows PowerShell 命令列介面 建立備份關聯。您必須改用 Lync Server 拓撲產生器指派備份集區。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPoolBackupRelationship"}

**Lync Server 控制台：** **Get-CsPoolBackupRelationship** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>要檢查備份關係之集區的完整網域名稱。例如：</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取備份關係資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsPoolBackupRelationship** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPoolBackupRelationship** Cmdlet 會傳回 Microsoft.Rtc.Management.Hadr.BackupService.BackupRelation 物件的執行個體。

