---
title: Remove-CsBackupServiceConfiguration
TOCTitle: Remove-CsBackupServiceConfiguration
ms:assetid: 56bbf0a2-20cf-4f1e-b305-3521659eb909
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204903(v=OCS.15)
ms:contentKeyID: 49290964
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsBackupServiceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

將 Lync Server 2013 之備份服務組態設定的屬性重設為預設值。這些設定包括可以同時對備份服務進行 Windows Communication Framework 呼叫的數目上限，以及備份服務同步處理間隔的資訊。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsBackupServiceConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會重設 Lync Server 2013 的備份服務組態設定。請注意，即使 Lync Server 2013 只使用單一、全域的備份設定集合，您仍必須包含 Identity 參數：若未加入此參數，**Remove-CsBackupServiceConfiguration** Cmdlet 將會在繼續前先提示您輸入 Identity。

    Remove-CsBackupServiceConfiguration -Identity "global"

## 詳細描述

備份服務組態設定可用於管理 Lync Server 2013 中的集區備份。請注意，Lync Server 只可有一份全域的備份組態設定集合。這表示所有集區皆必須使用相同的同步排程進行備份，而且有權存取備份集區 A 的使用者與群組，也有權存取備份集區 B、C、D 及 E。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsBackupServiceConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Remove-CsBackupServiceConfiguration** Cmdlet 所執行的功能。

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>備份服務組態設定的唯一 Identity。雖然您只能有這些設定的單一、全域執行個體，但是在呼叫 <strong>Remove-CsBackupServiceConfiguration</strong> Cmdlet 時，仍需要指定 Identity。</p>
<p>-Identity global</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
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
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Remove-CsBackupServiceConfiguration** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.BackupService.BackupServiceConfiguration 物件執行個體。

## 傳回類型

無。反之，**Remove-CsBackupServiceConfiguration** Cmdlet 會刪除 Microsoft.Rtc.Management.WritableConfig.Settings.BackupService.BackupServiceConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsBackupServiceConfiguration](get-csbackupserviceconfiguration.md)  
[Set-CsBackupServiceConfiguration](set-csbackupserviceconfiguration.md)

