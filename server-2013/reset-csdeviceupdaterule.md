---
title: Reset-CsDeviceUpdateRule
TOCTitle: Reset-CsDeviceUpdateRule
ms:assetid: 0de47bcf-da8f-4dae-b293-3adac3c1acdb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398181(v=OCS.15)
ms:contentKeyID: 49290082
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Reset-CsDeviceUpdateRule

 

_**上次修改主題的時間：** 2015-03-09_

拒絕匯入系統的裝置更新規則。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Reset-CsDeviceUpdateRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Reset-CsDeviceUpdateRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會重設在服務 WebServer:atl-cs-001.litwareinc.com 上找到的裝置更新規則 d5ce3c10-2588-420a-82ac-dc2d9b1222ff9。

    Reset-CsDeviceUpdateRule -Identity service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9

## 範例 2

範例 2 會重設已針對 WebServer:atl-cs-001.litwareinc.com 服務設定的所有裝置更新規則。作法是先呼叫 **Get-CsDeviceUpdateRule** Cmdlet 並搭配 Filter 參數；篩選值 "WebServer:atl-cs-001.litwareinc.com\*" 可確保只會傳回 Identity 開頭字元為 "WebServer:atl-cs-001.litwareinc.com" 的規則 (根據定義，這些是指派給 WebServer:atl-cs-001.litwareinc.com 服務的所有裝置更新規則)。然後再將篩選後集合管線傳送到 **Reset-CsDeviceUpdateRule** Cmdlet，以重設集合中的每個規則。

    Get-CsDeviceUpdateRule -Filter service:WebServer:atl-cs-001.litwareinc.com*  | Reset-CsDeviceUpdateRule

## 範例 3

範例 3 所示的命令會重設品牌 LG-Nortel 的所有裝置更新規則。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsDeviceUpdateRule** Cmdlet，以傳回組織目前所使用之所有裝置更新規則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Brand 屬性等於 LG-Nortel 的規則。接著將篩選後的集合管線傳送到 **Reset-CsDeviceUpdateRule** Cmdlet，以繼續重設篩選過的集合中的所有規則。

    Get-CsDeviceUpdateRule | Where-Object {$_.Brand -eq "LG-Nortel"} | Reset-CsDeviceUpdateRule

## 詳細描述

Lync Server 使用裝置更新規則來提供韌體更新給執行 Lync Phone Edition 的裝置。系統管理員會定期將一組裝置更新規則上傳到 Lync Server。在測試和核准這些規則之後，便會自動下載這些規則，並在適當裝置連線至系統時套用到這些裝置。根據預設，裝置每次開啟並連線到 Lync Server 時，都會檢查新的更新規則。在最初登入之後，裝置每隔 24 小時也會檢查一次更新。

每個新增至系統的新裝置更新規則都會標示為「擱置」。這表示適當的測試裝置將會下載並安裝更新，不過，通常不是由用戶端裝置進行下載並安裝。這可讓您有機會測試更新，並且先確認沒有負面影響，然後才廣泛提供此更新。在您確信更新已通過測試且適用於您的組織之後，接著就可以使用 **Approve-CsDeviceUpdateRule** Cmdlet 來核准更新。

另一方面，系統管理員也可能斷定組織中不應該使用指定更新 (例如，該更新可能使內部軟體發生衝突)。在該情況下，系統管理員可以使用 **Reset-CsDeviceUpdateRule** Cmdlet 來拒絕更新。當此情況發生時，更新規則的 PendingVersion 會設為 Null 值。然後，這表示登入系統的測試裝置將會解除安裝更新，並重新安裝該更新的核准版本。因為更新從未經由核准，這表示除了這些測試裝置，其他裝置絕對不會安裝更新。因此，不會影響一般使用者族群。

**Reset-CsDeviceUpdateRule** Cmdlet 只能用於「擱置」狀態中的裝置更新規則。如果某個規則已經過核准，您將必須使用 **Restore-CsDeviceUpdateRule** Cmdlet 回復裝置更新的部署。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Reset-CsDeviceUpdateRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Reset-CsDeviceUpdateRule"}

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
<td><p>隱藏當執行 Cmdlet 時可能發生的任何確認提示或非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要重設之裝置更新規則的唯一識別碼。裝置更新規則的 Identity 包含兩個部分：接受裝置更新規則指派的服務 (如 service:WebServer:atl-cs-001.litwareinc.com) 和全域唯一識別碼 (GUID)。因此，針對 Redmond 網站設定的裝置更新規則將擁有類似以下的 Identity：&quot;service:WebServer:atl-cs-oo1.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>DeviceUpdate.Rule</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule 物件。**Reset-CsDeviceUpdateRule** Cmdlet 接受管線傳送的裝置更新規則物件執行個體。

## 傳回類型

無。反之 **Reset-CsDeviceUpdateRule** Cmdlet 會重設 Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule 物件的執行個體。

## 請參閱

#### 其他資源

[Approve-CsDeviceUpdateRule](approve-csdeviceupdaterule.md)  
[Get-CsDeviceUpdateRule](get-csdeviceupdaterule.md)  
[Remove-CsDeviceUpdateRule](remove-csdeviceupdaterule.md)  
[Restore-CsDeviceUpdateRule](restore-csdeviceupdaterule.md)

