---
title: Backup-CsPool
TOCTitle: Backup-CsPool
ms:assetid: 66ec46de-e1e7-4e33-961d-7ef785059c48
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204955(v=OCS.15)
ms:contentKeyID: 49291161
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Backup-CsPool

 

_**上次修改主題的時間：** 2015-03-09_

建立指定 Lync Server 2013 集區的備份複本。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Backup-CsPool -PoolFqdn <Fqdn> [-Category <UserData | CMS>] [-Confirm [<SwitchParameter>]] [-FailedOverPoolOnly <SwitchParameter>] [-Force <SwitchParameter>] [-FullBackup <SwitchParameter>] [-LocalStore <SwitchParameter>] [-Report <String>] [-RetryCount <Int32>] [-SteadyState <SwitchParameter>] [-WaitTime <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會備份 atl-cs-001.litwareinc.com 集區。

    Backup-CsPool -PoolFqdn "atl-cs-001.litwareinc.com"

## 範例 2

範例 2 會為 atl-cs-001.litwareinc.com 集區進行「穩定狀態」備份。

    Backup-CsPool -PoolFqdn "atl-cs-001.litwareinc.com" -SteadyState

## 詳細描述

**Backup-CsPool** Cmdlet 可讓系統管理員將登錄器集區的使用者資料與會議資料複製到指定的備份集區。當主要集區失敗或變成無法使用時，位於主要集區上的使用者可以容錯移轉到備份集區。接著，這些使用者可以經由備份集區登入 Lync Server，以在主集區還原之前繼續使用該集區。

若要傳回所有指派給此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Backup-CsPool"}

**Lync Server 控制台**： Lync Server 控制台不提供 **Backup-CsPool** Cmdlet 所執行的功能。

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
<td><p>進行備份之集區的完整網域名稱。例如：</p>
<p>-SourcePoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Category</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Hadr.BackupService.BackupCategory</p></td>
<td><p>可讓您選取所要備份的 Lync Server 模組：若未指定此參數，將會備份所有模組。允許的值為：</p>
<p>* CMS</p>
<p>* UserData</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>FailedOverPoolOnly</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定此參數時，唯有當集區處於容錯移轉狀態，才會執行備份。如果您使用此參數，則也必須使用 FullBackup 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>FullBackup</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，要等到備份服務達到其最後狀態，才會開始備份。您無法在同一個命令中同時使用 FullBackup 參數和 SteadyState 參數。</p></td>
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
<td><p>在 Cmdlet 執行時所建立之記錄檔的檔案路徑。例如：</p>
<p>-Report &quot;C:\Logs\BackupPool.html&quot;</p>
<p>執行此 Cmdlet 時，若此檔案已存在，便會加以覆寫。</p>
<p>根據預設，報告會寫入至使用者設定檔中的 AppData\Local\Temp 資料夾。</p></td>
</tr>
<tr class="odd">
<td><p><em>RetryCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>Backup-CsPool 嘗試呼叫備份服務的次數上限，超過此上限即失敗。</p></td>
</tr>
<tr class="even">
<td><p><em>SteadyState</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，要等到備份服務達到穩定狀態，才會開始備份。當集區切換至唯讀或容錯移轉/容錯回復模式，而且不再產生需要備份的任何新資料時，就會出現「穩定狀態」。</p></td>
</tr>
<tr class="odd">
<td><p><em>WaitTime</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Cmdlet 在檢查備份服務處於完整狀態或穩定狀態之前所要等待的時間量 (以秒為單位)。</p></td>
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

無。 **Backup-CsPool** Cmdlet 不接受管線傳送的資料。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Get-CsBackupServiceConfiguration](get-csbackupserviceconfiguration.md)  
[Get-CsBackupServiceStatus](get-csbackupservicestatus.md)  
[Get-CsPoolBackupRelationship](get-cspoolbackuprelationship.md)

