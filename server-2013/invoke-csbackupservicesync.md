---
title: Invoke-CsBackupServiceSync
TOCTitle: Invoke-CsBackupServiceSync
ms:assetid: f3de25c2-a1ef-4781-8b33-74f5dc1e6f8d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205374(v=OCS.15)
ms:contentKeyID: 49292803
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsBackupServiceSync

 

_**上次修改主題的時間：** 2015-03-09_

手動叫用 Lync Server 2013集區及其指定的備份集區之間的備份同步作業。如此一來，系統管理員無須等候 Lync Server 複寫，即可同步資料。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Invoke-CsBackupServiceSync -PoolFqdn <Fqdn> [-BackupModule <String>] [-Force <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會同步處理集區 atl-cs-001.litwareinc.com 的備份服務。

    Invoke-CsBackupServiceSync -PoolFqdn "atl-cs-001.litwareinc.com"

## 詳細描述

**Invoke-CsBackupServiceSync** Cmdlet 可讓系統管理員同步登錄器集區及其備份集區的資料。**Invoke-CsBackupServiceSync** Cmdlet 只會複製保持兩個集區同步所需的資料。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsBackupServiceSync"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Invoke-CsBackupServiceSync** Cmdlet 所執行的功能。

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
<td><p>呼叫備份服務同步處理之集區的完整網域名稱。例如：</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>BackupModule</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>表示要同步處理的資料類型。有效值為：</p>
<p>* UserServices.PresenceFocus</p>
<p>* ConfServices.DataConf</p>
<p>* CentralMgmt.CMSMaster</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串值。**Invoke-CsBackupServiceSync** Cmdlet 可接受代表 Lync Server 2013 集區的完整網域名稱之管線傳送的字串值。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Backup-CsPool](backup-cspool.md)

