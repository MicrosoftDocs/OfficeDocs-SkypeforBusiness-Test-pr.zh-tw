---
title: Invoke-CsArchivingDatabasePurge
TOCTitle: Invoke-CsArchivingDatabasePurge
ms:assetid: 02310b08-736d-4ce9-91d8-5a6c8f323d7c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204627(v=OCS.15)
ms:contentKeyID: 49289905
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsArchivingDatabasePurge

 

_**上次修改主題的時間：** 2015-03-09_

手動清除封存資料庫中的記錄。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Invoke-CsArchivingDatabasePurge -Identity <XdsIdentity> <COMMON PARAMETERS>

    Invoke-CsArchivingDatabasePurge -SqlServerFqdn <String> [-SqlInstanceName <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -PurgeArchivingDataOlderThanHours <Int32> -PurgeExportedArchivesOnly <$true | $false> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-MaxArchivingRecordsToDelete <Int32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會從 atl-sql-001.litwareinc.com 上的封存資料庫中，清除留存時間超過 24 小時的所有記錄。為確保所有記錄 (包括尚未匯出的記錄) 皆能刪除，PurgeExportedArchivesOnly 參數會設為 False ($False)。

    Invoke-CsArchivingDatabasePurge -Identity "service:ArchivingDatabase:atl-sql-001.litwareinc.com" -PurgeArchivingDataOlderThanHours 24 -PurgeExportedArchivesOnly $False

## 範例 2

範例 2 所示的命令是範例 1 所示命令的變化，但此範例會使用下列語法新增 Confirm 參數：

\-Confirm:$False

該語法會隱藏清除封存記錄時所出現的確認提示。

    Invoke-CsArchivingDatabasePurge -Identity "service:ArchivingDatabase:atl-sql-001.litwareinc.com" -PurgeArchivingDataOlderThanHours 24 -PurgeExportedArchivesOnly $False -Confirm:$False

## 範例 3

範例 3 會從組織所使用的所有封存資料庫中，清除留存時間超過 24 小時的所有記錄。為達成此目的，範例中的第一個命令會使用 **Get-CsService** Cmdlet 及 ArchivingDatabase 參數傳回所有封存資料庫的集合。然後，此集合會管線傳送到 **ForEach-Object** Cmdlet。接著，ForEach-Object Cmdlet 會取用集合中的每個資料庫，並對資料庫執行 **Invoke-CsArchivingDatabasePurge** Cmdlet，以清除留存時間超過 24 小時的所有記錄。

    Get-CsService -ArchivingDatabase | ForEach-Object {Invoke-CsArchivingDatabasePurge -Identity $_.Identity -PurgeArchivingDataOlderThanHours 24 -PurgeExportedArchivesOnly $False -Confirm:$False}

## 詳細描述

許多組織會認為保留其使用者 (或選定的使用者子集) 所進行之各項 IM 工作階段的記錄有其實用性。另有一些組織則認為保留這些記錄有其必要性。例如依據法律規定，許多金融組織必須保留其所有的電子通訊複本。

若您的組織已啟用封存，並選擇使用 Lync Server 做為封存後端，則所有封存記錄將會存放在 SQL Server 資料庫 LcsLog 之中 (或者，也可改用 Microsoft Exchange 儲存封存記錄。如需詳細資訊，請參閱 **New-CsArchivingConfiguration** Cmdlet 的說明主題)。經過一段時間，封存資料庫可能會變得極大。有鑑於此，Lync Server 為系統管理員提供下列兩種方法清除資料庫中的舊記錄：1) 將 Lync Server 設定為每天自動刪除較舊的封存記錄；以及/或 2) 隨時使用 **Invoke-CsArchivingDatabasePurge** Cmdlet 刪除 LcsLog 資料庫中的封存記錄 (作法是由 **Invoke-CsArchivingDatabasePurge** Cmdlet 呼叫 SQL Server 的預存程序 RtcCleanupTempConference 與 RtcCleanupDB，然後刪除舊有的內容)。

當您呼叫 **Invoke-CsArchivingDatabasePurge** Cmdlet 時，必須指定用以儲存封存記錄之封存資料庫的位置 (例如 ArchivingDatabase:atl-sql-001.litwareinc.com)；另外還須指定刪除封存記錄前至少應保留的時間 (以小時為單位)。例如，若指定了 24 小時的最短保留時間，則資料庫中所有保留時間超過 24 小時的封存記錄皆會予以刪除。

請注意，即使指定的資料庫已停用清除功能 (亦即，封存組態設定中的 EnablePurging 屬性設為 False)，仍會刪除這些記錄。EnablePurging 屬性只可控制封存記錄的自動清除功能，對於 **Invoke-CsArchivingDatabasePurge** Cmdlet 沒有影響。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsArchivingDatabasePurge"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Invoke-CsArchivingDatabasePurge** Cmdlet 所執行的功能。

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
<td><p>要清除之封存資料庫的服務識別。您可以執行下列命令擷取封存資料庫的識別：</p>
<p>Get-CsService –ArchivingDatabase</p>
<p>請注意，請勿在同一個命令中同時使用 Identity 參數與 SqlServerFqdn 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>PurgeArchivingDataOlderThanHours</em></p></td>
<td><p>必要</p></td>
<td><p>System.Int32</p></td>
<td><p>指定要從資料庫中清除之封存記錄的存留時間 (小時)；存留時間超過此值的記錄皆會予以刪除。PurgeArchivingDataOlderThanHours 可設為 1 到 2147483647 的任何整數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeExportedArchivesOnly</em></p></td>
<td><p>必要</p></td>
<td><p>System.Boolean</p></td>
<td><p>如有指定此參數，將只會從封存資料庫移除已經匯出的記錄 (會將其標示為刪除)。尚未匯出的記錄會繼續保留在資料庫中，而無論其存留時間是否已超過 PurgeArchivingDataOlderThanHours 屬性所指定的值。</p></td>
</tr>
<tr class="even">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>封存資料庫所在之電腦的完整網域名稱。例如：</p>
<p>-SqlServerFqdn &quot;atl-sql-001.litwareinc.com&quot;</p>
<p>請注意，請勿在同一個命令中同時使用 Identity 參數與 SqlServerFqdn 參數。</p></td>
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
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxArchivingRecordsToDelete</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>指定要從資料庫清除的封存記錄數上限；如果將此值設為 99，而資料庫中有 100 筆符合 PurgeArchivingDataOlderThanHours 準則的記錄，將只會刪除最舊的 99 筆記錄。</p>
<p>MaxArchivingRecordsToDelete 可設為 1 到 2147483647 的任何整數值。</p></td>
</tr>
<tr class="even">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>封存資料庫的 SQL Server 執行個體名稱。例如：</p>
<p>-SqlInstanceName &quot;archinst&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Invoke-CsArchivingDatabasePurge** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.Xds.DisplayArchivingDatabase\#Decorated 類別執行個體。

## 傳回類型

Invoke-CsArchivingDatabasePurge Cmdlet 會傳回 Microsoft.Rtc.Management.Purge.ArchDataPurgeStatistics 類別的執行個體。

## 請參閱

#### 其他資源

[New-CsArchivingConfiguration](new-csarchivingconfiguration.md)  
[Set-CsArchivingConfiguration](set-csarchivingconfiguration.md)

