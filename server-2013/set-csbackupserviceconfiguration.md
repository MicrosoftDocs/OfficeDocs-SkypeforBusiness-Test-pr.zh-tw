---
title: Set-CsBackupServiceConfiguration
TOCTitle: Set-CsBackupServiceConfiguration
ms:assetid: 72ed064e-5f67-481f-802a-74846cecb189
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205006(v=OCS.15)
ms:contentKeyID: 49291301
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsBackupServiceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

擷取 Lync Server 2013 的備份服務組態設定，包括可以同時對備份服務進行 Windows Communication Framework 呼叫的數目上限，以及備份服務同步處理間隔的資訊。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsBackupServiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsBackupServiceConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AuthorizedLocalAccounts <String>] [-AuthorizedUniversalGroups <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-MaxBatchesPerCmsSync <Int32>] [-MaxBatchesPerUserStoreSync <Int32>] [-MaxConcurrentCalls <Int32>] [-MaxDataConfPackageSizeKB <Int32>] [-SyncInterval <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會針對全域的備份服務設定集合，將 Active Directory 安全性群組 Schema Admins 指派給 AuthorizedUniversalGroup 屬性。

    Set-CsBackupServiceConfiguration -Identity "global" -AuthorizedUniversalGroup "Schema Admins"

## 範例 2

範例 2 會將全域備份服務設定集合的 MaxConcurrentCalls 屬性會設為 12。

    Set-CsBackupServiceConfiguration -Identity "global" -MaxConcurrentCalls 12

## 範例 3

範例 3 會修改全域備份服務設定集合的 SyncInterval 屬性。在此範例中，SyncInterval 設為 10 分鐘：00 小時 : 10 分鐘 : 00 秒。

    Set-CsBackupServiceConfiguration -Identity "global" -SyncInterval "00:10:00"

## 詳細描述

備份服務組態設定可用於管理 Lync Server 2013 中的集區備份。請注意，Lync Server 只可有一份全域的備份組態設定集合。這表示所有集區皆必須使用相同的同步排程進行備份，而且有權存取備份集區 A 的使用者與群組，也有權存取備份集區 B、C、D 及 E。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsBackupServiceConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Set-CsBackupServiceConfiguration** Cmdlet 所執行的功能。

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
<td><p><em>AuthorizedLocalAccounts</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>經授權執行備份服務之本機使用者/本機群組的名稱。預設值為 Network Service。</p></td>
</tr>
<tr class="even">
<td><p><em>AuthorizedUniversalGroups</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>經授權執行備份服務之萬用群組的名稱。預設值為 Schema admins。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>備份服務組態設定的唯一識別碼。因為您只能有這些設定的單一、全域執行個體，所以在呼叫 <strong>Set-CsBackupServiceConfiguration</strong> Cmdlet 時，不需要指定 Identity。但是，您可以視需要使用下列語法來參照全域設定：</p>
<p>-Identity global</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參照傳遞給 Cmdlet，而非設定個別參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxBatchesPerCmsSync</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>CMS 備份模組將會在每個匯出周期間匯出的批次數目上限。預設值為 500。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxBatchesPerUserStoreSync</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>使用者存放區備份模組將會在每個匯出周期間匯出的批次數目上限。預設值為 500。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxConcurrentCalls</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>可以同時對備份服務進行的 Windows Communication Foundation (WCF) 呼叫數目上限。預設值為 10。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxDataConfPackageSizeKB</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>資料會議模組將會在每個匯出周期間匯出的資料封裝大小上限 (KB)。預設值為 102400。</p></td>
</tr>
<tr class="odd">
<td><p><em>SyncInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>指定服務等待多久之後，集區會與其備份集區同步處理。預設值為 2 分鐘 (00:02:00，亦即 00 小時，02 分鐘，00 秒)。SyncInterval 可設為 5 秒 (00:00:05) 到 3 小時 (03:00:00) (含) 之間的任何值。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Set-CsBackupServiceConfiguration** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.BackupService.BackupServiceConfiguration 物件執行個體。

## 傳回類型

無。反之，**Set-CsBackupServiceConfiguration** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.BackupService.BackupServiceConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsBackupServiceConfiguration](get-csbackupserviceconfiguration.md)  
[Remove-CsBackupServiceConfiguration](remove-csbackupserviceconfiguration.md)

