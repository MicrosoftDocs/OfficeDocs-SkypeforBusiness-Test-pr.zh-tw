---
title: Export-CsArchivingData
TOCTitle: Export-CsArchivingData
ms:assetid: 644bf86e-0e7e-4607-bedf-d491b1c16745
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398452(v=OCS.15)
ms:contentKeyID: 49291126
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsArchivingData

 

_**上次修改主題的時間：** 2015-03-09_

可讓您匯出儲存在 Lync Server封存資料庫中的記錄。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Export-CsArchivingData -DBInstance <String> -Identity <XdsIdentity> <COMMON PARAMETERS>

    Export-CsArchivingData -Identity <XdsIdentity> <COMMON PARAMETERS>

    Export-CsArchivingData -DBInstance <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -OutputFolder <String> -StartDate <DateTime> [-Confirm [<SwitchParameter>]] [-EndDate <DateTime>] [-ExcludeWebConfArchive <SwitchParameter>] [-Force <SwitchParameter>] [-IncludeTrustedApplication <SwitchParameter>] [-Purge <SwitchParameter>] [-UserUri <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會從位在 atl-sql-001.litwareinc.com 伺服器上的 封存資料庫擷取記錄，然後將產生的 EML 檔案儲存到 C:\\ArchivingExports 資料夾中。將開始日期指定為 2012 年 6 月 1 日 (-StartDate 6/1/2012) 可確保只將資料庫中於 2012 年 5 月 31 日之後記錄的項目匯出。

    Export-CsArchivingData -Identity "ArchivingDatabase:atl-sql-001.litwareinc.com" -StartDate 6/1/2012 -OutputFolder "C:\ArchivingExports"

## 範例 2

範例 2 是範例 1 所示之命令的變化；但在此範例中，只會匯出與使用者 Ken Myer 有關的記錄。若要將匯出的記錄限制在與單一使用者相關的記錄，請包含 UserUri 參數，後面加上適當的 SIP 位址。

    Export-CsArchivingData -Identity "ArchivingDatabase:atl-sql-001.litwareinc.com" -StartDate 6/1/2012 -OutputFolder "C:\ArchivingExports" -UserUri "kenmyer@litwareinc.com"

## 範例 3

範例 3 是範例 1 所示之命令的另一種變化，但在範例 3 中，只會匯出資料庫中在 2012 年 6 月期間記錄的項目。為了將匯出的項目限制在此時間間隔內，因此命令中同時包含了 EndDate 參數與 StartDate 參數。開始日期為 2012 年 6 月 1 日，結束日期為 2012 年 6 月 30 日，可將匯出項目限制在 2012 年 6 月記錄的項目。

    Export-CsArchivingData -Identity "ArchivingDatabase:atl-sql-001.litwareinc.com" -StartDate 6/1/2012 -EndDate 6/30/2012 -OutputFolder "C:\ArchivingExports"

## 詳細描述

許多組織發現將使用者所執行的所有立即訊息 (IM) 工作階段記錄保留下來是很有用的。也有其他組織發現這類記錄必須保留。例如，金融界的組織依法規定須保留其所有的電子通訊複本。

無論理由為何， Lync Server 讓您有彈性空間可封存 IM 與會議工作階段。若您已部署 封存伺服器，便能使用各種 **CsArchivingConfiguration** Cmdlet 來啟用及停用立即訊息的封存功能，以及管理 封存資料庫。如果封存失敗，您也可以暫停 IM；這有助於確保保留所有電子通訊的記錄。

如果您已啟用封存，則您的使用者電子通訊記錄會儲存在 封存資料庫 中。如果您想要檢視所有的記錄 (或檢視這些記錄的選取子集)，您可以使用 **Export-CsArchivingData** Cmdlet 從資料庫中擷取這些記錄，並儲存成 Outlook Express Electronic Mail (EML) 檔 (.EML 副檔名)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Export-CsArchivingData** Cmdlet：RTCComponentUniversalServices。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsArchivingData"}

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
<td><p><em>DBInstance</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>SQL Server 資料庫實體的路徑，封存資料記錄於該處。例如：&quot;atl-sql-001\Archinst&quot;。</p>
<p>此參數只可在 Microsoft Lync Server 2010 中使用。若要在 Lync Server 2013 中使用 <strong>Export-CsArchivingData</strong> Cmdlet，必須改用 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要匯出之封存資料庫的服務識別。例如：</p>
<p>-Identity &quot;ArchivingDatabase:atl-sql-001.litwareinc.com&quot;</p>
<p>您也可以直接使用集區名稱來指定資料庫：</p>
<p>-Identity &quot;atl-sql-001.litwareinc.com&quot;</p>
<p>您可以使用下列命令來擷取封存資料庫的服務識別：</p>
<p>Get-CsService –ArchivingDatabase | Select-Object Identity</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputFolder</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>應儲存所匯出資料的資料夾完整路徑 (例如 C:\ArchivingExports)。如果這個資料夾不存在，則 <strong>Export-CsArchivingData</strong> Cmdlet 便會建立該資料夾。</p></td>
</tr>
<tr class="even">
<td><p><em>StartDate</em></p></td>
<td><p>必要</p></td>
<td><p>System.DateTime</p></td>
<td><p>指出要匯出之記錄的最早活動日期。例如，如果您將開始日期設為 6/1/2010 (亦即 2010 年 6 月 1 日)，則在資料庫中任何該日期之前記錄的項目 (例如於 2010 年 5 月 31 日記錄的項目) 會於匯出時被排除。</p>
<p>指派值給 StartDate 和 EndDate 屬性時，請使用您的語言與地區選項設定所指定的日期時間格式。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>EndDate</em></p></td>
<td><p>選用</p></td>
<td><p>System.DateTime</p></td>
<td><p>指出要匯出之記錄的最晚活動日期。例如，如果您將結束日期設為 6/1/2010 (亦即 2010 年 6 月 1 日)，則在資料庫中任何該日期之後記錄的項目 (例如於 2010 年 6 月 2 日記錄的項目) 會於匯出時被排除。如果結束日期在開始日期之前 (例如結束日期為 1/1/2010，開始日期為 6/1/2010)，雖然您不會收到錯誤訊息，但匯出會失敗。</p>
<p>指派值給 StartDate 和 EndDate 屬性時，請使用您的語言與地區選項設定所指定的日期時間格式。</p>
<p>若未指定結束日期，系統會使用目前的日期。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludeWebConfArchive</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指示 <strong>Export-CsArchivingData</strong> Cmdlet 只匯出立即訊息記錄。根據預設，該 Cmdlet 會匯出 IM 與會議記錄。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>IncludeTrustedApplication</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>加入時，會指示 <strong>Export-CsArchivingData</strong> Cmdlet 在匯出記錄時，將信任的應用程式所記錄的資料包含在內。</p></td>
</tr>
<tr class="even">
<td><p><em>Purge</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果包含 Purge 參數，則會使任何已成功匯出的記錄自 封存資料庫 中刪除。如果未包含此參數，則匯出的記錄將保留在資料庫中。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您匯出單一使用者的封存資料；做法是使用 UserUri 參數並指定使用者的 SIP 位址。UserUri 參數一次只會接受一個 URI。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
<tr class="odd">
<td><p><em>DBInstance</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>SQL Server 資料庫實體的路徑，封存資料記錄於該處。例如：&quot;atl-sql-001\Archinst&quot;。</p>
<p>此參數只可在 Microsoft Lync Server 2010 中使用。若要在 Lync Server 2013 中使用 <strong>Export-CsArchivingData</strong> Cmdlet，必須改用 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要匯出之封存資料庫的服務識別。例如：</p>
<p>-Identity &quot;ArchivingDatabase:atl-sql-001.litwareinc.com&quot;</p>
<p>您也可以直接使用集區名稱來指定資料庫：</p>
<p>-Identity &quot;atl-sql-001.litwareinc.com&quot;</p>
<p>您可以使用下列命令來擷取封存資料庫的服務識別：</p>
<p>Get-CsService –ArchivingDatabase | Select-Object Identity</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputFolder</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>應儲存所匯出資料的資料夾完整路徑 (例如 C:\ArchivingExports)。如果這個資料夾不存在，則 <strong>Export-CsArchivingData</strong> Cmdlet 便會建立該資料夾。</p></td>
</tr>
<tr class="even">
<td><p><em>StartDate</em></p></td>
<td><p>必要</p></td>
<td><p>System.DateTime</p></td>
<td><p>指出要匯出之記錄的最早活動日期。例如，如果您將開始日期設為 6/1/2010 (亦即 2010 年 6 月 1 日)，則在資料庫中任何該日期之前記錄的項目 (例如於 2010 年 5 月 31 日記錄的項目) 會於匯出時被排除。</p>
<p>指派值給 StartDate 和 EndDate 屬性時，請使用您的語言與地區選項設定所指定的日期時間格式。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>EndDate</em></p></td>
<td><p>選用</p></td>
<td><p>System.DateTime</p></td>
<td><p>指出要匯出之記錄的最晚活動日期。例如，如果您將結束日期設為 6/1/2010 (亦即 2010 年 6 月 1 日)，則在資料庫中任何該日期之後記錄的項目 (例如於 2010 年 6 月 2 日記錄的項目) 會於匯出時被排除。如果結束日期在開始日期之前 (例如結束日期為 1/1/2010，開始日期為 6/1/2010)，雖然您不會收到錯誤訊息，但匯出會失敗。</p>
<p>指派值給 StartDate 和 EndDate 屬性時，請使用您的語言與地區選項設定所指定的日期時間格式。</p>
<p>若未指定結束日期，系統會使用目前的日期。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludeWebConfArchive</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指示 <strong>Export-CsArchivingData</strong> Cmdlet 只匯出立即訊息記錄。根據預設，該 Cmdlet 會匯出 IM 與會議記錄。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>IncludeTrustedApplication</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>加入時，會指示 <strong>Export-CsArchivingData</strong> Cmdlet 在匯出記錄時，將信任的應用程式所記錄的資料包含在內。</p></td>
</tr>
<tr class="even">
<td><p><em>Purge</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果包含 Purge 參數，則會使任何已成功匯出的記錄自 封存資料庫 中刪除。如果未包含此參數，則匯出的記錄將保留在資料庫中。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您匯出單一使用者的封存資料；做法是使用 UserUri 參數並指定使用者的 SIP 位址。UserUri 參數一次只會接受一個 URI。</p></td>
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

無。 **Export-CsArchivingData** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Export-CsArchivingData** Cmdlet 會以 EML 格式傳回 封存資料庫記錄。

## 請參閱

#### 其他資源

[Get-CsArchivingConfiguration](get-csarchivingconfiguration.md)

