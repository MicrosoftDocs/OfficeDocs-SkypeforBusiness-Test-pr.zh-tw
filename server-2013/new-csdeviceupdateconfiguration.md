---
title: New-CsDeviceUpdateConfiguration
TOCTitle: New-CsDeviceUpdateConfiguration
ms:assetid: 2a06450d-291e-40f9-a780-45e2c4b28494
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425761(v=OCS.15)
ms:contentKeyID: 49290401
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDeviceUpdateConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的裝置更新組態設定執行個體。這些設定可用於管理裝置更新 Web 服務。Lync Server 元件可讓系統管理員將韌體更新散發到電話及其他執行 Lync Server 的裝置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsDeviceUpdateConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-LogCleanUpInterval <TimeSpan>] [-LogCleanUpTimeOfDay <DateTime>] [-LogFlushInterval <TimeSpan>] [-MaxLogCacheLimit <UInt32>] [-MaxLogFileSize <UInt32>] [-ValidLogFileExtensions <PSListModifier>] [-ValidLogFileTypes <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立 Identity 為 site:Redmond 的新裝置更新組態設定集。由於命令中未加入其他任何參數，因此這個新組態設定集合將會針對每個屬性使用預設值。

    New-CsDeviceUpdateConfiguration -Identity site:Redmond

## 範例 2

範例 2 也會建立 Identity 為 site:Redmond 的新裝置更新組態設定集。在此情況下，使用了兩個額外的參數，以便自訂新設定：MaxLogFileSize 用來將記錄檔大小上限設為 2048000 個位元組，而加入 LogCleanUpInterval 用於將記錄清除間隔時間設為 7 天 (7 天 . 00 小時 : 00 分 : 00 秒)。

    New-CsDeviceUpdateConfiguration -Identity site:Redmond -MaxLogFileSize 204800 -LogCleanUpInterval 7.00:00:00

## 詳細描述

裝置更新 Web 服務提供方法讓系統管理員將韌體更新分送到執行 Lync Server 的裝置。系統管理員會定期將一組裝置更新規則上傳到 Lync Server。在測試和核准這些規則之後，便可在適當裝置連線至系統時套用到這些裝置。裝置在最初開啟電源時會檢查更新，然後在使用者登入時再次檢查。之後，裝置每隔 24 小時檢查一次更新。

用來管理裝置更新 Web 服務的裝置更新組態設定可指派到全域層級或網站範圍。若要為網站建立新設定集合，請使用 **New-CsDeviceUpdateConfiguration** Cmdlet。請注意，您只能在網站範圍建立新設定；如果嘗試在全域範圍建立新設定集合，則您的命令將會失敗。此外，如果嘗試建立 Redmond 網站之類的新設定集合，而且該網站已經裝載裝置更新組態設定集合，則您的命令將會失敗。那是因為每個網站只能有一個裝置更新組態設定集合。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsDeviceUpdateConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDeviceUpdateConfiguration"}

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
<td><p>表示新裝置更新組態設定的 Identity。由於只能在網站範圍建立新設定，因此 Identity 類似如下：-Identity &quot;site:Redmond&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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
<p>傳遞至 LogCleanupTimeOfDay 參數的值必須使用 24 小時時間格式 hh:mm，其中 hh 表示小時數，而 mm 表示分鐘數。在此格式中，午夜以 00:00 表示；8:30 A.M. 以 08:30 表示；11:52 P.M. 以 23:52 表示。預設值是 Null。</p></td>
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
<td><p>表示在必須清除快取並將資料寫入記錄檔之前，可保存在記錄檔快取中的資訊數量上限 (以位元組為單位)。根據預設，記錄檔每隔 X 分鐘便會「清除」(如需詳細資訊，請參閱參數 LogFlushInterval 的描述)。不過，如果快取達到其大小上限，其中的資訊將會自動寫入記錄檔 (而且會清除快取)，即使記錄清除間隔尚未到期也一樣。</p>
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
<td><p>表示可搭配 裝置更新 Web 服務 使用的有效記錄檔副檔名。此清單可以修改；不過，除非您執行 Lync Server 的裝置會建立使用不同副檔名的記錄檔，否則沒有什麼理由需要修改清單。</p>
<p>預設值：.dmp, .clg, .clg2, .bak, .kdmp, .dat, .bin, .cat, .xml, .txt, .hex</p></td>
</tr>
<tr class="odd">
<td><p><em>ValidLogFileTypes</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>表示裝置更新系統所保留的記錄檔類型。預設的檔案類型包括：</p>
<p>Watson。系統停止回應時，裝置自動產生的記錄檔。</p>
<p>CELog。執行 Lync 之電話的記錄，包含功能測試結果及重要系統事件記錄。</p>
<p>如果您的裝置 (執行 Lync Phone Edition) 會建立不同類型的記錄檔，則可以新增其他檔案類型。您也可以移除檔案。例如，如果您不要儲存 CELog 檔案，則可以移除 CELog 檔案類型。</p></td>
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

無。**New-CsDeviceUpdateConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsDeviceUpdateConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdateConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsDeviceUpdateConfiguration](get-csdeviceupdateconfiguration.md)  
[Remove-CsDeviceUpdateConfiguration](remove-csdeviceupdateconfiguration.md)  
[Set-CsDeviceUpdateConfiguration](set-csdeviceupdateconfiguration.md)

