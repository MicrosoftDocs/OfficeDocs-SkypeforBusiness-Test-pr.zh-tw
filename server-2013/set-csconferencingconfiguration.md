---
title: Set-CsConferencingConfiguration
TOCTitle: Set-CsConferencingConfiguration
ms:assetid: c468d7fd-fb2c-469c-85fb-58e0834aac36
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412969(v=OCS.15)
ms:contentKeyID: 49292239
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferencingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的會議組態設定集合。會議設定可指定會議內容與講義的大小上限、內容寬限期 (即內容刪除前所能儲存的時間)，以及支援之用戶端內部與外部下載的 URL 等事項。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsConferencingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsConferencingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ClientAppSharingPort <UInt16>] [-ClientAppSharingPortRange <UInt32>] [-ClientAudioPort <UInt16>] [-ClientAudioPortRange <UInt32>] [-ClientFileTransferPort <UInt16>] [-ClientFileTransferPortRange <UInt32>] [-ClientMediaPort <UInt16>] [-ClientMediaPortRange <UInt32>] [-ClientMediaPortRangeEnabled <$true | $false>] [-ClientSipDynamicPort <UInt16>] [-ClientSipDynamicPortRange <UInt32>] [-ClientVideoPort <UInt16>] [-ClientVideoPortRange <UInt32>] [-Confirm [<SwitchParameter>]] [-ConsoleDownloadExternalUrl <String>] [-ConsoleDownloadInternalUrl <String>] [-ContentGracePeriod <TimeSpan>] [-Force <SwitchParameter>] [-HelpdeskExternalUrl <String>] [-HelpdeskInternalUrl <String>] [-MaxBandwidthPerAppSharingServiceMb <UInt64>] [-MaxContentStorageMb <UInt16>] [-MaxUploadFileSizeMb <UInt16>] [-Organization <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中， **Set-CsConferencingConfiguration** Cmdlet 會修改會議組態設定的全域執行個體；在此案例中，命令會將 Organization 屬性的值設為 Litwareinc。作法是使用 Organization 參數加上 Litwareinc 組織名稱。

    Set-CsConferencingConfiguration -Identity global -Organization Litwareinc

## 範例 2

範例 2 是第一個範例的延伸。在此案例中，命令會針對目前使用的每一個會議組態設定修改 Organization 屬性值。為達成此目的，命令會先使用 **Get-CsConferencingConfiguration** Cmdlet，以擷取所有會議組態設定的集合。然後，此集合會以管線傳送到 **Set-CsConferencingConfiguration** Cmdlet，以取得集合中的每一個項目，並將 Organization 屬性的值變更為 Litwareinc。

    Get-CsConferencingConfiguration | Set-CsConferencingConfiguration -Organization Litwareinc

## 範例 3

範例 3 所示的命令可針對所有已套用至網站範圍的會議組態設定變更 MaxContentStorageMb 屬性的值。為達成此目的，命令會先呼叫 **Get-CsConferencingConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "site:\*" 可確保只會傳回 Identity 開頭為 "site:" 字元的設定。然後將篩選後的集合以管線傳送到 **Set-CsConferencingConfiguration** Cmdlet，以將集合中每一個項目的 MaxContentStorageMB 屬性值變更為 50。

    Get-CsConferencingConfiguration -Filter site:* | Set-CsConferencingConfiguration -MaxContentStorageMb 50 

## 範例 4

範例 4 會修改所有允許儲存 100 MB 以上之內容的會議組態設定，將允許儲存的內容上限設為 100 MB。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsConferencingConfiguration** Cmdlet，以傳回目前使用之所有會議組態設定的集合。然後，此集合會以管線傳送到 **Where-Object** Cmdlet，以選取 MaxContentStorageMB 屬性大於 100 的設定。接著將篩選後的集合以管線傳送到 **Set-CsConferencingConfiguration** Cmdlet，以取得集合中的每一個項目，並將 MaxContentStorageMb 屬性的值設為 100。

    Get-CsConferencingConfiguration | Where-Object {$_.MaxContentStorageMb -gt 100} | Set-CsConferencingConfiguration -MaxContentStorageMB 100

## 範例 5

範例 5 會擷取 Redmond 網站 (-Identity site:Redmond) 的會議組態設定，並且會修改 ContentGracePeriod 屬性的值，將寬限期設為 22 小時 (22 小時：00 分鐘：00 秒)。

    Set-CsConferencingConfiguration -Identity site:Redmond -ContentGracePeriod "22:00:00"

## 範例 6

範例 6 會修改所有未將 Fabrikam 列為 Organization 的會議組態設定。特別是，系統會將 Litwareinc 指派為這些設定的新組織。為了完成此工作，命令會先呼叫不含任何參數的 **Get-CsConferencingConfiguration** Cmdlet，以傳回組織目前使用之所有會議組態設定的集合。然後，此集合會以管線傳送到 **Where-Object** Cmdlet，以選取所有 Organization 屬性不等於 (-ne) Fabrikam 的設定。接著將篩選後的集合以管線傳送到 **Set-CsConferencingConfiguration** Cmdlet。 **Set-CsConferencingConfiguration** Cmdlet 會取得集合中的每一個項目，並將 Organization 屬性的值變更為 Litwareinc。

    Get-CsConferencingConfiguration | Where-Object {$_.Organization -ne "Fabrikam"} | Set-CsConferencingConfiguration -Organization Litwareinc

## 詳細描述

對於會議而言，管理與系統管理會分別以兩組 Cmdlet 進行。如果您想要管理使用者能做與不能做的事情 (例如，使用者是否可以邀請匿名參與者加入會議、使用者是否可以在會議內進行應用程式共用，或使用者是否可以在會議內傳輸檔案)，則需使用 **CsConferencingPolicy** Cmdlet。

除了管理使用者活動之外，系統管理員還需要管理 Web 會議服務。例如，系統管理員需要能夠執行一些動作，例如指定配置給單一會議的內容儲存量上限，以及指定自動刪除該會議內容之前的寬限期。他們也需要能夠指定諸如應用程式共用及檔案傳輸這類活動使用的連接埠。

後面的活動是使用 **CsConferencingConfiguration** Cmdlet 來管理的。這些 Cmdlet 可讓您管理實際伺服器本身。 **CsConferencingConfiguration** Cmdlet (可以套用至全域、網站及服務範圍) 雖然不能用來指定使用者是否可在會議期間共用應用程式，但是可以在允許應用程式共用時，用來指出該活動應該使用哪些連接埠。同樣地，Cmdlet 也可讓您指定一些事項，例如儲存限制和期限，以及可供使用者用來取得會議說明及資源的內部與外部 URL 指標。

安裝 Lync Server 時，系統會提供您一個會議組態設定集合 (全域集合)。如果您需要針對網站或服務建立自訂設定，可以使用 **New-CsConferencingConfiguration** Cmdlet 來進行作業。建立這些自訂設定後，您可以使用 **Set-CsConferencingConfiguration** Cmdlet 來修改其中的任何設定 (或修改全域集合)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsConferencingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferencingConfiguration"}

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
<td><p><em>ClientAppSharingPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>代表用於應用程式共用的起始連接埠號碼。ClientAppSharingPort 必須是介於 1024 到 65535 之間 (包括 1024 和 65535) 的連接埠號碼值。預設值為 5350。</p></td>
</tr>
<tr class="even">
<td><p><em>ClientAppSharingPortRange</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示可供應用程式共用使用的連接埠總數 (預設值為 40)。若要決定實際上用於應用程式共用的連接埠，請使用這個值和 ClientAppSharingPort 值。例如，如果將 ClientAppSharingPort 設為 5350、將 ClientAppSharingPortRange 設為 3，則下列 3 個連接埠都可供應用程式共用使用：5350; 5351; 5352。</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientAudioPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>代表用於用戶端音訊的起始連接埠號碼。ClientAudioPort 必須是介於 1024 到 65535 之間 (包括 1024 和 65535) 的連接埠號碼值。預設值為 5350。</p></td>
</tr>
<tr class="even">
<td><p><em>ClientAudioPortRange</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示可供用戶端音訊使用的連接埠總數 (預設值為 40)。若要決定實際上用於用戶端音訊的連接埠，請使用這個值和 ClientAudioPort 值。例如，如果將 ClientAudioPort 設為 5350、將 ClientAudioPortRange 設為 3，則下列 3 個連接埠都可供用戶端音訊使用：5350; 5351; 5352。</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientFileTransferPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>代表用於檔案傳輸的起始連接埠號碼。ClientFileTransferPort 必須是介於 1024 到 65535 之間 (包括 1024 和 65535) 的連接埠號碼值。預設值為 5350。</p></td>
</tr>
<tr class="even">
<td><p><em>ClientFileTransferPortRange</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示可供檔案傳輸使用的連接埠總數 (預設值為 40)。若要決定實際上用於檔案傳輸的連接埠，請使用這個值和 ClientFileTransferPort 值。例如，如果將 ClientFileTransferPort 設為 5350、將 ClientFileTransferPortRange 設為 3，則下列 3 個連接埠都可供檔案傳輸使用：5350; 5351; 5352。</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientMediaPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>代表用於用戶端媒體的起始連接埠號碼。此參數適用於 Microsoft Office Communicator 2007 R2 用戶端。ClientMediaPort 必須是介於 1024 到 65535 (包括 1024 和 65535) 之間的連接埠號碼值。預設值為 5350。</p></td>
</tr>
<tr class="even">
<td><p><em>ClientMediaPortRange</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示可供用戶端媒體使用的連接埠總數 (預設值為 40)。此參數適用於 Office Communicator 2007 R2 用戶端。若要決定實際上用於用戶端媒體的連接埠，請使用這個值和 ClientMediaPort 值。例如，如果將 ClientMediaPort 設為 5350、將 ClientMediaPortRange 設為 3，則下列三個連接埠都可供用戶端媒體使用：5350; 5351; 5352。</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientMediaPortRangeEnabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，用戶端將使用指定的連接埠範圍來傳輸媒體流量。設為 False (預設值) 時，系統會使用連接埠 1024 到連接埠 65535 之間任何可用的連接埠來容納媒體流量。</p></td>
</tr>
<tr class="even">
<td><p><em>ClientSipDynamicPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>代表用於 SIP 流量的起始連接埠號碼。ClientSipDynamicPort 必須是介於 1024 到 65535 之間 (包括 1024 和 65535) 的連接埠號碼值。預設值為 7100。</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientSipDynamicPortRange</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示可供 SIP 流量使用的連接埠總數 (預設值為 3)。若要決定實際上用於 SIP 流量的連接埠，請使用這個值和 ClientSipDynamicPort 值。例如，如果將 ClientSipDynamicPort 設為 7100、將 ClientSipDynamicPortRange 設為 3，則下列 3 個連接埠都可供用戶端媒體使用：7100; 7101; 7102。</p></td>
</tr>
<tr class="even">
<td><p><em>ClientVideoPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>代表用於用戶端視訊的起始連接埠號碼。ClientVideoPort 必須是介於 1024 到 65535 之間 (包括 1024 和 65535) 的連接埠號碼值。預設值為 5350。</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientVideoPortRange</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示可供用戶端視訊使用的連接埠總數 (預設值為 40)。若要決定實際上用於用戶端視訊的連接埠，請使用這個值和 ClientVideoPort 值。例如，如果將 ClientVideoPort 設為 5350、將 ClientVideoPortRange 設為 3，則下列 3 個連接埠都可供用戶端視訊使用：5350; 5351; 5352。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>ConsoleDownloadExternalUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>供外部使用者下載支援 Lync 2013 等用戶端的 URL。請注意，此設定僅適用於登入 Lync Server 集區的舊版用戶端 (例如 Microsoft Office Communicator 2007 R2)。</p></td>
</tr>
<tr class="even">
<td><p><em>ConsoleDownloadInternalUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>供內部使用者下載支援 Lync 2013 等用戶端的 URL。請注意，此設定僅適用於登入 Lync Server 集區的舊版用戶端 (例如 Microsoft Office Communicator 2007 R2)。</p></td>
</tr>
<tr class="odd">
<td><p><em>ContentGracePeriod</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>表示會議結束後，會議內容存留在伺服器中的時間。您必須以下列格式指定 ContentGracePeriod：天數.小時數:分鐘數:秒數。例如，若要將內容寬限期設為 30 天，請使用下列語法：-ContentGracePeriod 30.00:00:00。</p>
<p>您可以將內容寬限期設為 30 分鐘 (00:30:00) 到 180 天 (180.00:00:00) 之間的任何值。預設值為 15 天 (15.00:00:00)。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>HelpdeskExternalUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>外部使用者在會議中點擊 [說明] 時，系統會引導該使用者前往的 URL。</p></td>
</tr>
<tr class="even">
<td><p><em>HelpdeskInternalUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>內部使用者在會議中點擊 [說明] 時，系統會引導該使用者前往的 URL。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之會議組態設定集合的唯一識別碼。若要參照全域集合，請使用下列語法：-Identity global。若要參照在此網站範圍設定的集合，請使用如下語法：-Identity &quot;site:Redmond&quot;。若要在服務範圍內參照某個集合，請使用下列語法：-Identity &quot;service:ConferencingServer:atl-cs-001.litwareinc.com&quot;。 Web 會議服務是唯一能主控這些組態設定的服務。</p>
<p>如果未指定此參數，則 <strong>Set-CsConferencingConfiguration</strong> Cmdlet 將會自動修改全域設定。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>ConfSettings 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxBandwidthPerAppSharingServiceMb</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>表示為 應用程式共用會議服務預留的頻寬上限 (MB)。您可以將 MaxBandwidthPerAppSharingServiceMb 設為 50 到 100000 之間 (包括 50 和 100000) 的任何整數值。預設值為 375 MB。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxContentStorageMb</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>允許供儲存會議內容的檔案空間上限 (MB)。您可以將 MaxContentStorageMb 設為 50 到 1024 (1 GB) 之間 (包括 50 和 1024) 的任何整數值。預設值為 500 MB。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxUploadFileSizeMb</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>指定會議可以使用的檔案大小總計上限 (包含講義和 PowerPoint 投影片)。在 Microsoft Exchange Server 中封存會議內容時，一般會使用此設定：透過設定上傳檔案大小上限，您可以確保在會議中使用的內容 (必須封存此內容) 不超過為 Microsoft Exchange 設定的檔案大小上限。預設值為 500 MB。</p></td>
</tr>
<tr class="even">
<td><p><em>Organization</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>主控會議之組織的名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings 物件。 **Set-CsConferencingConfiguration** Cmdlet 接受會議組態物件以管線傳送的執行個體。

## 傳回類型

**Set-CsConferencingConfiguration** Cmdlet 不會傳回值或物件。反之，Cmdlet 會設定 Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsConferencingConfiguration](get-csconferencingconfiguration.md)  
[New-CsConferencingConfiguration](new-csconferencingconfiguration.md)  
[Remove-CsConferencingConfiguration](remove-csconferencingconfiguration.md)

