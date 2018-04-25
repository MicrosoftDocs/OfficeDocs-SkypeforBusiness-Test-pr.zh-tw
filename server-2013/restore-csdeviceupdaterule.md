---
title: Restore-CsDeviceUpdateRule
TOCTitle: Restore-CsDeviceUpdateRule
ms:assetid: 4c89d529-23fc-470e-9006-f15a18ed13fd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398305(v=OCS.15)
ms:contentKeyID: 49290847
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Restore-CsDeviceUpdateRule

 

_**上次修改主題的時間：** 2015-03-09_

可讓您「還原」通過核准供組織使用的裝置更新規則。當您還原裝置更新規則時，會將核准版本的規則重設為規則核准前的狀態。然後登入系統的用戶端裝置會自動解除安裝最近的更新，再下載並重新安裝該更新的上一個版本。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Restore-CsDeviceUpdateRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Restore-CsDeviceUpdateRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會還原在服務 WebServer:atl-cs-001.litwareinc.com 上找到的裝置更新規則 d5ce3c10-2588-420a-82ac-dc2d9b1222ff9。

    Restore-CsDeviceUpdateRule -Identity service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9

## 範例 2

範例 2 會還原已針對 WebServer:atl-cs-001.litwareinc.com 服務設定的所有裝置更新規則。作法是先呼叫 **Get-CsDeviceUpdateRule** Cmdlet 並搭配 Filter 參數；篩選值 "WebServer:atl-cs-001.litwareinc.com\*" 可確保只會傳回 Identity 開頭字元為 "WebServer:atl-cs-001.litwareinc.com" 的規則 (根據定義，這些是指派給 WebServer:atl-cs-001.litwareinc.com 服務的所有裝置更新規則)。然後再將篩選後的集合管線傳送到 **Restore-CsDeviceUpdateRule** Cmdlet，以還原集合中的每一個規則。

    Get-CsDeviceUpdateRule -Filter service:WebServer:atl-cs-001.litwareinc.com* | Restore-CsDeviceUpdateRule

## 範例 3

範例 3 會示範如何還原指定品牌 (LG-Nortel) 的所有裝置更新規則。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsDeviceUpdateRule** Cmdlet，以傳回組織目前所使用之所有裝置更新規則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Brand 屬性等於 LG-Nortel 的規則。接著將篩選後的集合管線傳送到 **Restore-CsDeviceUpdateRule** Cmdlet，以還原篩選過之集合中的所有規則。

    Get-CsDeviceUpdateRule | Where-Object {$_.Brand -eq "LG-Nortel"} | Restore-CsDeviceUpdateRule

## 詳細描述

Lync Server 使用裝置更新規則來提供韌體更新給執行 Lync Phone Edition 的裝置。系統管理員會定期將一組裝置更新規則上傳至 Lync Server；當那些規則經過測試並核准之後，如果這些裝置下次連線至系統，系統就會自動下載那些規則並套用至相關裝置上。根據預設，每當裝置開啟，並連線至 Lync Server 時，就會檢查新的更新規則；裝置在該初始登入之後，也會每 24 小時檢查一次更新。

每個新增至系統的新裝置更新規則都會標示為「擱置」。這表示適當的測試裝置將會下載並安裝更新，不過，通常不是由用戶端裝置進行下載並安裝。這可讓您有機會測試更新，並且先確認沒有負面影響，然後才廣泛提供此更新。在您確信更新已通過測試且適用於您的組織之後，接著就可以使用 **Approve-CsDeviceUpdateRule** Cmdlet 來核准更新。

核准更新時，系統會將相關更新規則的 PendingVersion 指派給 ApprovedVersion，並清除 PendingVersion 屬性。例如，假設新更新規則的 PendingVersion 是 1.0.0.1 版。在執行 **Approve-CsDeviceUpdateRule** Cmdlet 之後，系統會將 PendingVersion 設為 Null 值，並將 ApprovedVersion 設為 1.0.0.1。下次用戶端裝置檢查是否有更新時，將會自動下載並安裝更新。

除此之外，任何舊版的更新 (例如，1.0.0.0 版) 將會標示為 RestoreVersion。這一版的更新將會保留在系統上，而且如果新更新需要回復時，將會使用它。如果開始出現問題，系統管理員可以使用 **Restore-CsDeviceUpdateRule** Cmdlet 回復更新。發生該情況時，下次用戶端裝置檢查是否有更新時，裝置會自動解除安裝新的更新 (1.0.0.1 版)，並重新安裝上一版更新 (1.0.0.0)。

請注意，當然，只有要安裝上一版更新時才會發生這種情況。如果沒有上一版更新，則回復更新時便只是單純解除安裝。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Restore-CsDeviceUpdateRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Restore-CsDeviceUpdateRule"}

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
<td><p>要還原之裝置更新的唯一識別碼。裝置更新規則的 Identity 包含兩個部分：接受裝置更新規則指派的服務 (如 service:WebServer:atl-cs-001.litwareinc.com) 和全域唯一識別碼 (GUID)。因此，針對 Redmond 網站設定的裝置更新規則將擁有類似以下的 Identity：service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>DeviceUpdate.Rule 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule 物件。**Restore-CsDeviceUpdateRule** Cmdlet 接受管線傳送的裝置更新規則物件執行個體。

## 傳回類型

無。反之，**Restore-CsDeviceUpdateRule** Cmdlet 會還原 Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule 物件的執行個體。

## 請參閱

#### 其他資源

[Approve-CsDeviceUpdateRule](approve-csdeviceupdaterule.md)  
[Get-CsDeviceUpdateRule](get-csdeviceupdaterule.md)  
[Remove-CsDeviceUpdateRule](remove-csdeviceupdaterule.md)  
[Reset-CsDeviceUpdateRule](reset-csdeviceupdaterule.md)

