---
title: Set-CsDeviceUpdateConfiguration
TOCTitle: Set-CsDeviceUpdateConfiguration
ms:assetid: 4f200a03-984a-4c5b-a9c1-a866ba1851cd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398320(v=OCS.15)
ms:contentKeyID: 49290889
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDeviceUpdateConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改裝置更新 Web 服務組態設定的集合。這些設定可用於管理裝置更新 Web 服務。Lync Server 元件可讓系統管理員將韌體更新散發到電話及其他執行 Lync Server 的裝置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsDeviceUpdateConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsDeviceUpdateConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-LogCleanUpInterval <TimeSpan>] [-LogCleanUpTimeOfDay <DateTime>] [-LogFlushInterval <TimeSpan>] [-MaxLogCacheLimit <UInt32>] [-MaxLogFileSize <UInt32>] [-ValidLogFileExtensions <PSListModifier>] [-ValidLogFileTypes <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會示範如何使用 **Set-CsDeviceUpdateConfiguration** Cmdlet 修改全域組態設定。在此範例中，修改了兩個屬性值：MaxLogFileSize 屬性設為 2048000 個位元組，而 MaxLogCacheLimit 屬性設為 1024000 個位元組。

    Set-CsDeviceUpdateConfiguration -Identity global -MaxLogFileSize 2048000 -MaxLogCacheLimit 1024000

## 範例 2

範例 2 會修改 Identity 為 site:Redmond 之裝置更新組態設定的 LogFlushInterval 屬性。為達此目的，命令會使用 Identity 參數來指定 Redmond 網站的設定，並使用 LogFlushInterval 參數指示要變更的屬性值。在此情況下，LogFlushInterval 設為 2 分鐘 (00 時: 02 分: 00 秒)。

    Set-CsDeviceUpdateConfiguration -Identity site:Redmond -LogFlushInterval 00:02:00

## 範例 3

範例 3 會修改組織中的所有裝置組態更新設定，以將 LogCleanUpInterval 設為 14 天。為達成此目的，會先使用 **Get-CsDeviceUpdateConfiguration** Cmdlet 擷取目前所使用之所有裝置更新組態設定的集合。然後，此集合會管線傳送到 **Set-CsDeviceUpdateConfiguration** Cmdlet，以使用 LogCleanUpInterval 參數將集合中每個項目的記錄檔清除間隔時間設為 14 天 (14 天。00 小時：00 分：00 秒)。

    Get-CsDeviceUpdateConfiguration | Set-CsDeviceUpdateConfiguration -LogCleanUpInterval 14.00:00:00

## 範例 4

範例 4 會示範如何修改已在網站範圍設定之所有裝置更新組態設定的屬性值；在此範例中，命令會將 LogCleanUpInterval 設為 20 天 (20 天。00 小時：00 分：00 秒)。為達成此目的，會使用 **Get-CsDeviceUpdateConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "site:\*" 可將傳回的資料限制在 Identity 開頭字串值為 "site:" 的設定。然後再將篩選後的集合管線傳送到 **Set-CsDeviceUpdateConfiguration** Cmdlet，以變更集合中每個項目的記錄檔清除間隔值。

    Get-CsDeviceUpdateConfiguration -Filter "site:*" | Set-CsDeviceUpdateConfiguration -LogCleanUpInterval 20.00:00:00

## 範例 5

範例 5 會將 CELog 從裝置更新組態設定所使用的有效記錄檔類型清單中移除。此命令會先使用 **Get-CsDeviceUpdateConfiguration** Cmdlet 擷取組織目前所使用之所有裝置更新組態設定的集合。然後，此集合會管線傳送到 **Set-CsDeviceUpdateConfiguration** Cmdlet，以使用 ValidLogFileTypes 參數將 CELog 從有效記錄檔類型清單中移除。傳遞到 ValidLogFileTypes 的 @{Remove="CELog"} 參數值會指示 **Set-CsDeviceUpdateConfiguration** Cmdlet 從有效檔案類型集中移除 CELog。若要在單一命令中移除多個檔案類型，只要以逗號分隔清單的方式加入其他類型即可。例如：

@{Remove="CELog","Watson"}

    Get-CsDeviceUpdateConfiguration | Set-CsDeviceUpdateConfiguration -ValidLogFileTypes @{Remove="CELog"}

## 詳細描述

裝置更新 Web 服務提供方法讓系統管理員將韌體更新分送到執行 Lync Phone Edition 的裝置。系統管理員會定期將一組裝置更新規則上傳到 Lync Server。在測試和核准這些規則之後，便可在適當裝置連線至系統時套用到這些裝置。裝置在最初開啟電源時會檢查更新，然後在使用者登入時再次檢查。裝置之後也會每 24 小時檢查一次更新。

裝置更新組態設定可以在全域範圍或網站範圍套用。**Set-CsDeviceUpdateConfiguration** Cmdlet 可讓您變更設定集合。例如，您可以使用此 Cmdlet 變更系統自動刪除記錄檔之前，保留記錄檔的時間長度)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsDeviceUpdateConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDeviceUpdateConfiguration"}

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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
<td><p>要修改之裝置更新組態設定的唯一識別碼。若要參考全域設定，請使用下列語法：-Identity global。若要參考網站設定，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。請注意，如有指定 Identity，即無法使用萬用字元。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>DeviceUpdateSettings 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>LogCleanUpInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>指定保留裝置更新記錄檔的時間，此時間之後，系統會將其刪除。</p>
<p>此值必須以 dd.hh:mm:ss 格式輸入，其中 dd 為天數、hh 為小時數、mm 為分鐘數、ss 為秒數。若只輸入天數，則該值之後必須加上句號 (.)。</p>
<p>最小值：1.00:00:00 (1 天)</p>
<p>最大值：365.00:00:00 (1 年)</p>
<p>預設值：10.00:00:00 (10 天)</p></td>
</tr>
<tr class="even">
<td><p><em>LogCleanUpTimeOfDay</em></p></td>
<td><p>選用</p></td>
<td><p>System.DateTime</p></td>
<td><p>表示系統檢查是否有任何應該刪除之過期記錄檔的天數 (「過期」記錄檔是指比 LogCleanupInterval 屬性中指定之值更舊的任何檔案)。</p>
<p>傳遞至 LogCleanupTimeOfDay 參數的值應該使用 24 小時時間格式 hh:mm，其中 hh 表示小時數，而 mm 表示分鐘數。在這個格式中，00:00 表示午夜；08:30 表示 8:30 A.M，而 23:52 表示 11:52 P.M.。</p></td>
</tr>
<tr class="odd">
<td><p><em>LogFlushInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>表示儲存在記錄檔快取中的資訊寫入實際記錄檔的頻率。根據預設，裝置更新資訊不會立即寫入記錄檔；但是，該資訊會快取於記憶體中，直到：1) 記錄清除時間間隔已過期；或者 2) 快取已達大小上限。如果此值設為 10 分鐘 (00:10:00)，則快取中的資訊將會每隔 10 分鐘寫入記錄檔。當資料經過記錄之後，便會清除快取。</p>
<p>此值必須以 hh:mm:ss 格式輸入，其中 hh 為小時數、mm 為分鐘數、ss 為秒數。</p>
<p>最小值：00:01:00 (1 分鐘)</p>
<p>最大值：1:00:00 (1 小時)</p>
<p>預設值：00:05:00</p></td>
</tr>
<tr class="even">
<td><p><em>MaxLogCacheLimit</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示在必須清除快取並將資料寫入記錄檔之前，可保存在記錄檔快取中的資訊數量上限 (以位元組為單位)。根據預設，記錄檔每隔 5 分鐘便會「清除」。(如需詳細資訊，請參閱參數 LogFlushInterval 的說明)。不過，如果快取達到其大小上限，其中的資訊將會自動寫入記錄檔 (而且會清除快取)，即使記錄清除間隔尚未到期也一樣。</p>
<p>預設值：512000</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxLogFileSize</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示個別記錄檔的大小上限 (以位元組為單位)。當檔案達到大小上限時，下一個批次的資料會自動寫入新記錄檔。舊記錄檔將會保留，直到記錄清除間隔已到期為止。</p>
<p>預設值：1024000</p></td>
</tr>
<tr class="even">
<td><p><em>ValidLogFileExtensions</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>表示可搭配裝置更新 Web 服務使用的有效記錄檔副檔名。此清單可以修改；不過，除非您所擁有的 Lync Phone Edition 相容裝置會建立使用不同副檔名的記錄檔，否則沒有什麼理由需要修改清單。</p>
<p>預設值：.dmp, .clg, .clg2, .bak, .kdmp, .dat, .bin, .cat, .xml, .txt, .hex</p></td>
</tr>
<tr class="odd">
<td><p><em>ValidLogFileTypes</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>表示裝置更新系統所保留的記錄檔類型。預設的檔案類型包括：</p>
<p>Watson。系統損毀時，裝置自動產生的記錄檔。</p>
<p>CELog。包含功能測試結果及重要系統事件記錄的 Lync Phone 記錄。</p>
<p>如果您所擁有的 Lync Phone Edition 相容裝置會建立不同種類的記錄檔，則可以新增其他檔案類型。您也可以移除檔案。例如，如果您不要儲存 CELog 檔案，則可以移除 CELog 檔案類型。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdateConfiguration 物件。**Set-CsDeviceUpdateConfiguration** Cmdlet 接受管線傳送的裝置更新組態物件執行個體。

## 傳回類型

**Set-CsDeviceUpdateConfiguration** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdateConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsDeviceUpdateConfiguration](get-csdeviceupdateconfiguration.md)  
[New-CsDeviceUpdateConfiguration](new-csdeviceupdateconfiguration.md)  
[Remove-CsDeviceUpdateConfiguration](remove-csdeviceupdateconfiguration.md)

