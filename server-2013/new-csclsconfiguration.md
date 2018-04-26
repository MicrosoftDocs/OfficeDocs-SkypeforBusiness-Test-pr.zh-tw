---
title: New-CsClsConfiguration
TOCTitle: New-CsClsConfiguration
ms:assetid: 44cf1720-feae-47a5-b56a-5891a095b243
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619177(v=OCS.15)
ms:contentKeyID: 49290761
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClsConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的集中式記錄組態設定集合。集中式記錄提供一種方法，讓管理員同時啟用或停用多部電腦上的 Lync Server 2013 追蹤功能。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsClsConfiguration -Identity <XdsIdentity> [-CacheFileLocalFolders <String>] [-CacheFileLocalMaxDiskUsage <UInt32>] [-CacheFileLocalRetentionPeriod <UInt32>] [-CacheFileNetworkFolder <String>] [-ComponentThrottleLimit <UInt32>] [-ComponentThrottleSample <UInt32>] [-Confirm [<SwitchParameter>]] [-EtlFileFolder <String>] [-EtlFileRolloverMinutes <UInt32>] [-EtlFileRolloverSizeMB <UInt32>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MinimumClsAgentServiceVersion <UInt32>] [-Regions <PSListModifier>] [-Scenarios <PSListModifier>] [-SearchTerms <PSListModifier>] [-SecurityGroups <PSListModifier>] [-TmfFileSearchPath <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會針對 Redmond 網站建立新的集中式記錄組態設定集合。在這個新集合中，ETL 檔案變換大小設定為 40 MB，而 ETL 檔案變換時間設定為 2 小時 (120 分鐘)。

    New-CsClsConfiguration -Identity "site:Redmond" -EtlFileRolloverSizeMB 40 -EtlFileRolloverMinutes 120

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

集中式記錄是以一系列預先定義的案例為主來建立，可提供比舊版 Lync Server 更精確的記錄方法。這些案例可為您預先決定伺服器元件與記錄功能；因此，啟用 RGS 案例的管理員確信將只會記錄與「回應群組」服務有關的資訊，而非不相關的服務，例如音訊會議提供者服務。

您也可以使用 [New-CsClsScenario](new-csclsscenario.md) Cmdlet，定義自訂的案例。

您可以使用集中式記錄服務組態設定的集合來管理集中式記錄。 當您安裝 Lync Server 2013 時，就會安裝一組這類的全域組態設定；此外，管理員可以在網站範圍新增自訂的設定集合。只要使用 **New-CsClsConfiguration** Cmdlet 即可。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClsConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **New-CsCClsConfiguration** Cmdlet 所執行的功能。

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
<td><p>要建立之集中式記錄組態設定的唯一識別碼。因為這些設定只能在網站範圍上建立，所以使用類似如下含前置字元 &quot;site:&quot; 的語法，後面再加上網站的名稱：</p>
<p>-Identity &quot;site:Redmond&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>CacheFileLocalFolders</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>儲存快取檔案之本機資料夾的一或多個完整路徑。預設值為 %TEMP%\Tracing。如果指定多個路徑，請用分號加以分隔。</p></td>
</tr>
<tr class="odd">
<td><p><em>CacheFileLocalMaxDiskUsage</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>快取檔案可用的磁碟空間上限 (百分比)。預設值為 80。</p></td>
</tr>
<tr class="even">
<td><p><em>CacheFileLocalRetentionPeriod</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>可在本機保留快取檔案的天數上限。預設值為 14。</p></td>
</tr>
<tr class="odd">
<td><p><em>CacheFileNetworkFolder</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>網路快取資料夾的完整 UNC 路徑。沒有預設值。</p></td>
</tr>
<tr class="even">
<td><p><em>ComponentThrottleLimit</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>調節元件追蹤之前，允許元件產生追蹤記錄的速率上限。預設值是每秒 5000 次追蹤通話。</p></td>
</tr>
<tr class="odd">
<td><p><em>ComponentThrottleSample</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>在一分鐘的間隔內，可超過 ComponentThrottleLimit 的次數上限。預設值是 3。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EtlFileFolder</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>儲存事件記錄追蹤檔案的資料夾完整路徑。預設值為 %TEMP%\Tracing。請注意，因為是在 CLS 服務的內容中評估 %TEMP%，所以它其實會展開為 %WINDIR%\ServiceProfiles\NetworkService\AppData\Local</p></td>
</tr>
<tr class="even">
<td><p><em>EtlFileRolloverMinutes</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>在建立新的事件記錄追蹤檔案前的最長等待時間 (以分鐘為單位)。(即使現有的追蹤檔案未達指定的變換大小，仍將會建立這個新檔案。) 預設值為 60。</p></td>
</tr>
<tr class="odd">
<td><p><em>EtlFileRolloverSizeMB</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>在建立新檔案之前，事件追蹤記錄檔案可達的大小上限 (以 MB 為單位)。預設值為 20。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>MinimumClsAgentServiceVersion</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>指定記錄資料時要使用之集中式記錄服務代理程式的最低版本；記錄作業會將執行代理程式版本低於最小值的任何電腦排除。預設值為 6，代表 Lync Server 2013。此參數適用於 商務用 Skype Online。</p></td>
</tr>
<tr class="odd">
<td><p><em>Regions</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>針對集中式記錄組態設定而定義的地區集合。地區是使用 New-CsClsRegion Cmdlet 定義而成。</p>
<p>此參數適合與 Lync Server 2013 搭配使用。</p></td>
</tr>
<tr class="even">
<td><p><em>Scenarios</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>元件/情況的集合可以使用集中式記錄來追蹤。案例可使用 <strong>CsClsScenario</strong> Cmdlets 來管理。</p></td>
</tr>
<tr class="odd">
<td><p><em>SearchTerms</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>搜尋集中式記錄檔案的技術支援人員，可使用能協助判斷個人識別資訊的字詞集合。搜尋字詞可以使用 <strong>CsClsSearchTerm</strong> Cmdlets來管理。</p></td>
</tr>
<tr class="even">
<td><p><em>SecurityGroups</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>允許存取記錄檔案的安全性群組。</p>
<p>此參數適合與 商務用 Skype Online 搭配使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>TmfFileSearchPath</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>TMF (追蹤訊息格式) 檔案的搜尋路徑。TMF 檔案可將二進位追蹤訊息轉換成人類看得懂的格式。</p></td>
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

無。**New-CsClsConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsClsConfiguration** Cmdlet 會建立新的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.CentralizedLoggingConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsClsConfiguration](get-csclsconfiguration.md)  
[Remove-CsClsConfiguration](remove-csclsconfiguration.md)  
[Set-CsClsConfiguration](set-csclsconfiguration.md)

