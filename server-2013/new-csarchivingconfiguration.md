---
title: New-CsArchivingConfiguration
TOCTitle: New-CsArchivingConfiguration
ms:assetid: 66cab8b7-c3b3-4c1b-a77a-28f295ff6010
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398471(v=OCS.15)
ms:contentKeyID: 49291160
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsArchivingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的立即訊息 (IM) 封存設定集合。這些設定可用於啟用或停用 IM 工作階段的自動儲存功能，同時也可讓您封鎖無法封存的立即訊息。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsArchivingConfiguration -Identity <XdsIdentity> [-ArchiveDuplicateMessages <$true | $false>] [-BlockOnArchiveFailure <$true | $false>] [-CachePurgingInterval <UInt32>] [-Confirm [<SwitchParameter>]] [-EnableArchiving <None | ImOnly | ImAndWebConf>] [-EnableExchangeArchiving <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-KeepArchivingDataForDays <UInt32>] [-PurgeExportedArchivesOnly <$true | $false>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立新的封存組態設定集合，並將這些設定套用到 Redmond 網站。透過加入 EnableArchiving 參數並將參數值設為 "ImOnly"，此命令也可以針對 Redmond 網站啟用 IM 工作階段封存 (但非 Web 會議封存)。

    New-CsArchivingConfiguration -Identity site:Redmond -EnableArchiving "ImOnly"

## 範例 2

範例 2 會示範如何使用 InMemory 參數來建立一開始只存在於記憶體中的封存組態設定集合。為達成此目的，此範例會建立一個新的設定集合 (其 Identity 為 site:Redmond)，並將此集合儲存在名稱為 $x 的變數中。請注意，在第一個命令執行後，該集合只會存在於記憶體中；如果您執行 **Get-CsArchivingConfiguration** Cmdlet，將看不到 site:Redmond 的項目。

在第二個命令中，此虛擬設定集合的 EnableArchiving 屬性會設為 "ImOnly"，以啟用 IM 工作階段封存。最後，最後一個命令會使用 **Set-CsArchivingConfiguration** Cmdlet，將該虛擬封存設定轉換為套用到 Redmond 網站的實際設定集合。如果您沒有呼叫 **Set-CsArchivingConfiguration** Cmdlet，這些設定將只會保留在記憶體中，而且一旦終止 Windows PowerShell 工作階段或刪除變數 $x，這些設定就會消失。

    $x = New-CsArchivingConfiguration -Identity site:Redmond -InMemory
    $x.EnableArchiving = "ImOnly"
    Set-CsArchivingConfiguration -Instance $x

## 詳細描述

許多組織都發現保留使用者執行之所有 IM 工作階段的文字記錄相當實用。對於某些組織而言，保留此類文字記錄是強制性的；例如，許多財務組織都依法保留其所有電子通訊的副本。

就封存 IM 和網路會議工作階段而言，Lync Server 可讓您根據需求彈性地選擇。如果您已部署 封存伺服器，便能使用各種 **CsArchivingConfiguration** Cmdlet 來啟用及停用 IM 工作階段的封存功能，以及管理您的封存資料庫。而在封存失敗時，您也可以藉由暫停 IM 來確保所有電子通訊均能納入記錄。

當您安裝 Lync Server 時，將會為您建立全域封存設定集合；根據預設，這些設定將會套用到整個組織。或者，您可以使用 **New-CsArchivingConfiguration** Cmdlet，根據個別網站建立自訂組態設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsArchivingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsArchivingConfiguration"}

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
<td><p>表示要指派給封存組態設定之新集合的唯一識別碼。在 Lync Server 2013 中，您可以在網站範圍或服務範圍建立新的集合。(在 Microsoft Lync Server 2010 中，您只可以在網站範圍建立這些設定。) 若要在網站範圍建立新的設定，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若要在服務範圍建立設定 (只限針對登錄器服務)，請使用類似下列的語法︰</p>
<p>-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>ArchiveDuplicateMessages</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指定如何封存跨集區的立即訊息。例如，Ken Myer (在集區 1 中有帳戶) 傳送立即訊息給 Pilar Ackerman (在集區 2 中有帳戶)。接著 Pilar 會針對 Ken 的立即訊息傳送回覆。如果 ArchiveDuplicateMessages 設為 False，則 (根據內建演算法) 工作階段文字記錄將會記錄在集區 1 或集區 2 中，但不會同時記錄在兩個集區中。如果 ArchiveDuplicateMessages 設為 True (預設值)，則文字記錄將會記錄在兩個集區中。</p></td>
</tr>
<tr class="odd">
<td><p><em>BlockOnArchiveFailure</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，則每次無法封存立即訊息工作階段時，就會暫停 IM 服務。如果設為 False (預設值)，則即使無法封存工作階段，立即訊息也會繼續。</p></td>
</tr>
<tr class="even">
<td><p><em>CachePurgingInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示沒有任何參與者啟用封存時，系統清除文字記錄的頻率 (小時)。依設計，當所有群組 IM 工作階段與會議工作階段進行時，都會進行記錄。系統會在指定的間隔判斷是否有任何參與者在這些工作階段中啟用封存。如果系統發現其中沒有任何參與者啟用封存的工作階段，則會從資料庫刪除該文字記錄。</p>
<p>CachePurgeInterval 屬性可以設為 4 和 168 (含) 之間的任何整數值。預設值為 24。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableArchiving</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.EnableArchiving</p></td>
<td><p>表示要儲存到封存資料庫的項目 (如果有的話)。有效值為：</p>
<p>None。沒有項目封存到資料庫。此為預設值。</p>
<p>ImOnly。IM 工作階段封存到資料庫。</p>
<p>ImAndWebConf。會將 IM 和 Web 會議工作階段封存至資料庫。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableExchangeArchiving</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，Lync Server 2013立即訊息和會議文字記錄會儲存在 Microsoft Exchange Server 2013，而不是分開的 SQL Server 資料庫中。請注意，如有啟用 Exchange 封存，將則會以 Exchange 封存原則 (而不是 Lync Server 封存原則) 管理使用者。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePurging</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，將會定期從資料庫移除已封存的立即訊息，但前提是，這些立即訊息：1) 舊於在 KeepArchivingDataForDays 屬性中指定的值；或 2) 已遭到匯出並標示為刪除。</p>
<p>若為 False，立即訊息將不會從資料庫自動刪除。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>抑制顯示執行命令時可能引起的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepArchivingDataForDays</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>在已封存的立即訊息遭到自動刪除前，保留在資料庫中的天數 (1 和 2562 之間)。預設值為 14。</p>
<p>只有在 EnablePurging 設為 True 時，這個屬性才會生效。</p></td>
</tr>
<tr class="even">
<td><p><em>PurgeExportedArchivesOnly</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，則系統將只會清除已經匯出 (因此標示為刪除) 的立即訊息。即使立即訊息舊於 KeepArchivingDataForDays 屬性所指定的值，但尚未匯出的這些訊息還是會保留在資料庫中。</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示一天中過期的記錄從封存資料庫中刪除的時間。一天中的時間是以 24 小時制指定，其中 0 表示午夜 (12:00 AM)，而 23 表示 11:00 PM。請注意，您僅能指定一天中的小時數。也就是說，您可以排程在 4:00 AM 進行清除，但是您無法排程在 4:30 AM 或 4:15 AM 進行清除。預設值為 2 (2:00 AM)。</p>
<p>只有在 EnablePurging 屬性設為 True 時，才會進行資料庫清除。</p></td>
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

無。**New-CsArchivingConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsArchivingConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.ArchivingSettings 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsArchivingConfiguration](get-csarchivingconfiguration.md)  
[Remove-CsArchivingConfiguration](remove-csarchivingconfiguration.md)  
[Set-CsArchivingConfiguration](set-csarchivingconfiguration.md)  
[Set-CsArchivingServer](set-csarchivingserver.md)

