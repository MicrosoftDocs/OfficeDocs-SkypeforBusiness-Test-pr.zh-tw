---
title: Get-CsBackupServiceConfiguration
TOCTitle: Get-CsBackupServiceConfiguration
ms:assetid: 8e81a76c-4019-490d-9cd5-895cc2cc0863
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205087(v=OCS.15)
ms:contentKeyID: 49291620
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsBackupServiceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

擷取 Lync Server 2013 的備份服務組態設定，包括可以同時對備份服務進行 Windows Communication Framework 呼叫的數目上限，以及備份服務同步處理間隔的資訊。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsBackupServiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsBackupServiceConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會擷取 Lync Server 2013的備份服務組態資訊。因為只有單一、全域的備份服務組態設定集合，所以在執行此命令時，不需要包含 Identity 參數。

    Get-CsBackupServiceConfiguration

## 詳細描述

備份服務組態設定可用於管理 Lync Server 2013 中的集區備份。請注意，Lync Server 只可有一份全域的備份組態設定集合。這表示所有集區皆必須使用相同的同步排程進行備份，而且有權存取備份集區 A 的使用者與群組，也有權存取備份集區 B、C、D 及 E。

Get-CsBackupServiceConfiguration 可從任何執行 Lync Server 2013 伺服器角色的電腦或 Windows PowerShell 的遠端執行個體執行。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsBackupServiceConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Get-CsBackupServiceConfiguration** Cmdlet 所執行的功能。

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您在參照備份服務組態設定集合時，使用萬用字元值。因為您只能有這些設定的單一、全域執行個體，所以沒有理由使用 Filter 參數。不過，如果您想要，可以使用下列語法來參照全域設定：</p>
<p>-Filter &quot;g*&quot;</p>
<p>上述語法會傳回以 &quot;g&quot; 字母為開頭的所有會議備份服務組態設定。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>備份服務組態設定的唯一 Identity。因為您只能有這些設定的單一、全域執行個體，所以在呼叫 <strong>Get-CsBackupServiceConfiguration</strong> Cmdlet 時，不需要指定 Identity。然而，您可以使用下列語法來參照全域設定︰</p>
<p>-Identity global</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取備份服務組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsBackupServiceConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsBackupServiceConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.BackupService.BackupServiceConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[Remove-CsBackupServiceConfiguration](remove-csbackupserviceconfiguration.md)  
[Set-CsBackupServiceConfiguration](set-csbackupserviceconfiguration.md)

