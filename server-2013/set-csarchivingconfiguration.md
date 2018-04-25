---
title: Set-CsArchivingConfiguration
TOCTitle: Set-CsArchivingConfiguration
ms:assetid: f5202dc2-b3b4-48ae-93d2-d19e71847994
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413030(v=OCS.15)
ms:contentKeyID: 49292823
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsArchivingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的立即訊息 (IM) 封存設定集合。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsArchivingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsArchivingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ArchiveDuplicateMessages <$true | $false>] [-BlockOnArchiveFailure <$true | $false>] [-CachePurgingInterval <UInt32>] [-Confirm [<SwitchParameter>]] [-EnableArchiving <None | ImOnly | ImAndWebConf>] [-EnableExchangeArchiving <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-KeepArchivingDataForDays <UInt32>] [-PurgeExportedArchivesOnly <$true | $false>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會使用 **Set-CsArchivingConfiguration** Cmdlet 修改 Identity 為 site:Redmond 之封存組態設定的兩個屬性。首先，命令會將 ArchiveDuplicateMessages 屬性設為 False，以防止伺服器多次封存相同的立即訊息工作階段。命令也會使用 KeepArchivingDataForDays 參數指示伺服器，將立即訊息保留 30 天。

    Set-CsArchivingConfiguration -Identity site:Redmond -ArchiveDuplicateMessages $False -KeepArchivingDataForDays 30

## 範例 2

範例 2 是範例 1 所示指令的的變化：但在此例中，會針對已設定於網站範圍上的所有封存設定來修改 ArchiveDuplicateMessages 和 KeepArchivingDataForDays 屬性的值。為了執行此工作，命令會先使用 **Get-CsArchivingConfiguration** Cmdlet 及 Filter 參數，以傳回設定在網站範圍之所有封存設定的集合；篩選值 "site:\*" 會確保設定的 Identity 開頭字元為 "site"：才會傳回。然後將篩選過的集合管線傳送到 **Set-CsArchivingConfiguration** Cmdlet，這會修改集合中每一個項目的兩個屬性值。

    Get-CsArchivingConfiguration -Filter "site:*" | Set-CsArchivingConfiguration -ArchiveDuplicateMessages $False -KeepArchivingDataForDays 30

## 範例 3

範例 3 會修改所有同時允許 IM 工作階段和 Web 會議封存的封存組態設定；當此命令完成之後，就只會針對 IM 工作階段封存允許這些設定。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsArchivingConfiguration** Cmdlet，以傳回組織目前所使用之所有封存組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 EnableArchiving 屬性等於 (-eq) "ImAndWebConf" 的設定。接著將篩選後的集合管線傳送到 **Set-CsArchivingConfiguration** Cmdlet，以取得集合中的每個項目，並將 EnableArchiving 的值變更為 "ImOnly"。

    Get-CsArchivingConfiguration | Where-Object {$_.EnableArchiving -eq "ImAndWebConf"} | Set-CsArchivingConfiguration -EnableArchiving "ImOnly"

## 詳細描述

有許多組織認為，保留使用者參與之所有 IM 工作階段和會議的記錄是相當有用的。另外，也有一些組織會強制保留這些記錄。例如，根據法律規定，許多金融界的組織都必須保留所有電子通訊的副本。

為了封存立即訊息，您必須至少設定一個 封存伺服器。設定封存伺服器之後，您必須執行兩個額外的步驟。首先，需要在全域範圍上啟用封存 (如需詳細資訊，請參閱 **Set-CsArchivingConfiguration** Cmdlet 說明主題)。或者，也可以針對不同網站設定自訂的封存設定。

其次，您必須使用封存原則，指出將要封存其 IM 工作階段的使用者。不會封存 IM 工作階段，除非使用需要封存 IM 工作階段的原則。

在安裝 Lync Server 時，系統會為您建立全域封存組態設定集合。根據預設，這些設定會套用至整個組織。或者，您也可以使用 **New-CsArchivingConfiguration** Cmdlet 來針對各個網站建立自訂的組態設定。無論如何，您都可以使用 **Set-CsArchivingConfiguration** Cmdlet 修改現有集合或封存組態設定的屬性值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsArchivingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsArchivingConfiguration"}

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
<td><p><em>ArchiveDuplicateMessages</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指定應如何封存「跨集區」立即訊息。假設一個簡單範例：Ken Myer (在集區 1 中擁有一個帳戶) 傳送立即訊息給 Pilar Ackerman (在集區 2 中擁有一個帳戶)；接著 Pilar 傳送一則立即訊息來回覆 Ken。如果 ArchiveDuplicateMessages 已設定為 False，則 (根據內建的演算法) 工作階段記錄將記錄於集區 1 或集區 2 中，但不會同時記錄於兩者中。如果 ArchiveDuplicateMessages 已設定為 True (預設值)，記錄將同時記錄於這兩個集區中。</p></td>
</tr>
<tr class="even">
<td><p><em>BlockOnArchiveFailure</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，則 IM 服務隨時都會因為無法封存立即訊息而暫停。若設定為 False (預設值)，即使無法封存立即訊息，IM 都將繼續執行。</p></td>
</tr>
<tr class="odd">
<td><p><em>CachePurgingInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>指出系統清除記錄的頻率 (以小時為單位)，其中並未啟用任何參與者來進行封存。根據設計，所有群組 IM 工作階段和會議工作階段都會在執行時加以記錄。系統會在指定的時間間隔判斷這些工作階段中的任何參與者是否已啟用來進行封存。如果系統發現某個工作階段中並未啟用任何參與者來進行封存，則將從資料庫中刪除該記錄。</p>
<p>CachePurgingInterval 屬性可以設定為任何介於 4 和 168 (含) 之間的整數值。預設值為 24。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableArchiving</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.EnableArchiving</p></td>
<td><p>指出要將哪些項目 (如果有的話) 儲存至封存資料庫。有效值為：</p>
<p>None。不會將任何項目封存至資料庫。此為預設值。</p>
<p>ImOnly。會將 IM 工作階段封存至資料庫。</p>
<p>ImAndWebConf。會將 IM 和 Web 會議工作階段封存至資料庫。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableExchangeArchiving</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，Lync Server 2013立即訊息和會議文字記錄會儲存在 Microsoft Exchange Server 2013，而不是個別的 SQL Server 資料庫上。請注意，如果啟用 Exchange 封存，則使用者會受 Exchange 封存原則管理，而不是受 Lync Server 2013封存原則管理。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePurging</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，則當封存的立即訊息符合下列條件時，即會定期從資料庫移除這些立即訊息：1) 較 KeepArchivingDataForDays 屬性中指定的值還舊；或者，2) 已匯出並標記為刪除。</p>
<p>若為 False，將不會自動從資料庫刪除立即訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>代表要修改之封存組態設定集合的唯一識別碼。若要修改全域設定，請省略此參數或使用下列語法：-Identity global。若要修改網站範圍上的設定，請使用 &quot;site:&quot; 首碼，後面加上網站名稱。例如：-Identity &quot;site:Redmond&quot;。</p>
<p>若要修改指派至個別登錄器集區 (只有 Lync Server 2013 中有此功能) 的設定，請使用類似下列的語法：</p>
<p>-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>ArchivingSettings 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepArchivingDataForDays</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>在自動刪除封存的立即訊息之前，這類立即訊息應於資料庫中保留的天數 (介於 1 和 2562 之間)。預設值為 14。</p>
<p>唯有當 EnablePurging 已設定為 True 時，此屬性才會生效。</p></td>
</tr>
<tr class="even">
<td><p><em>PurgeExportedArchivesOnly</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，則系統將只會清除已匯出 (因而已標記為刪除) 的立即訊息。尚未匯出的立即訊息將保留於資料庫中，即使這些立即訊息較 KeepArchivingDataForDays 屬性指定的值還舊也一樣。</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>指出要在一天中的哪個時間從封存資料庫刪除到期的記錄。時間是以 24 小時制指定，0 代表午夜 (12:00 AM)，而 23 則代表 11:00 PM。請注意，只能指定一天中的小時。這表示您可以排程要在 4:00 AM 執行清除，但無法將之排程為在 4:30 AM 或 4:15 AM (舉例來說) 執行。預設值為 2 (2:00 AM)。</p>
<p>只有在 EnablePurging 屬性設為 True 時，才會進行資料庫清除作業。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.ArchivingSettings 物件。**Set-CsArchivingConfiguration** Cmdlet 會接受封存組態物件的管線傳送資料。

## 傳回類型

**Set-CsArchivingConfiguration** Cmdlet 不會傳回值或物件，而是會設定 Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.ArchivingSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsArchivingConfiguration](get-csarchivingconfiguration.md)  
[New-CsArchivingConfiguration](new-csarchivingconfiguration.md)  
[Remove-CsArchivingConfiguration](remove-csarchivingconfiguration.md)  
[Set-CsArchivingServer](set-csarchivingserver.md)

