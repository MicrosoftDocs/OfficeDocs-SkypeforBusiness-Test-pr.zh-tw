---
title: Approve-CsDeviceUpdateRule
TOCTitle: Approve-CsDeviceUpdateRule
ms:assetid: d82e0494-4868-4d13-ac03-e5a5d0f2380e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398949(v=OCS.15)
ms:contentKeyID: 49292490
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Approve-CsDeviceUpdateRule

 

_**上次修改主題的時間：** 2015-03-09_

核准匯入系統的裝置更新規則。當裝置更新規則通過後，受更新影響的用戶端裝置將會自動下載及安裝對應的更新。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Approve-CsDeviceUpdateRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Approve-CsDeviceUpdateRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會核准 WebServer:atl-cs-001.litwareinc.com 服務中的 d5ce3c10-2588-420a-82ac-dc2d9b1222ff9 裝置更新規則。

    Approve-CsDeviceUpdateRule -Identity service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9

## 範例 2

範例 2 會核准針對 WebServer:atl-cs-001.litwareinc.com 服務設定的所有裝置更新規則。作法是先呼叫 **Get-CsDeviceUpdateRule** Cmdlet 並搭配 Filter 參數；篩選值 "WebServer:atl-cs-001.litwareinc.com\*" 可確保只會傳回 Identity 開頭字元為 "WebServer:atl-cs-001.litwareinc.com" 的規則 (根據定義，這些是指派給 WebServer:atl-cs-001.litwareinc.com 服務的所有裝置更新規則)。然後將此篩選後的集合管線傳送到 **Approve-CsDeviceUpdateRule** Cmdlet，以核准集合中的每一個規則。

    Get-CsDeviceUpdateRule -Filter service:WebServer:atl-cs-001.litwareinc.com* | Approve-CsDeviceUpdateRule

## 範例 3

範例 3 所示的命令會核准指定品牌 (LG-Nortel) 的所有裝置更新規則。為達成此目的，命令會先呼叫 **Get-CsDeviceUpdateRule** Cmdlet，以傳回組織目前使用的所有裝置更新規則集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Brand 屬性等於 LG-Nortel 的規則。接著將篩選後的集合管線傳送到 **Approve-CsDeviceUpdateRule** Cmdlet，以核准集合中的每一個規則。

    Get-CsDeviceUpdateRule | Where-Object {$_.Brand -eq "LG-Nortel"} | Approve-CsDeviceUpdateRule

## 詳細描述

Lync Server 使用裝置更新規則來提供韌體更新給執行 Lync Phone Edition 的裝置。系統管理員會定期將一組裝置更新規則上傳到 Lync Server；那些規則經過測試與核准後，裝置與系統連線時會自動下載並套用到裝置。根據預設，每當裝置開啟並連接至 Lync Server 時，都會檢查新的更新規則。在最初登入之後，裝置每隔 24 小時也會檢查一次更新。

每個新增至系統的新裝置更新規則都會標示為「擱置」。這表示適當的測試裝置將會下載並安裝更新，不過，通常不是由用戶端裝置進行下載並安裝。這可讓您有機會測試更新，並且先確認沒有負面影響，然後才廣泛提供此更新。在您確信更新已通過測試且適用於您的組織之後，接著就可以使用 **Approve-CsDeviceUpdateRule** Cmdlet 來核准更新。

核准更新時，系統會將相關更新規則的 PendingVersion 指派給 ApprovedVersion，並清除 PendingVersion 屬性。例如，假設新更新規則的 PendingVersion 是 1.0.0.1 版。在執行 **Approve-CsDeviceUpdateRule** Cmdlet 之後，系統會將 PendingVersion 設為 Null 值，並將 ApprovedVersion 設為 1.0.0.1。等到下次用戶端裝置登入時，裝置便會自動檢查是否有任何適用該裝置的新核准更新。如果有的話，將會自動下載並安裝更新。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Approve-CsDeviceUpdateRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Approve-CsDeviceUpdateRule"}

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
<td><p>待核准之裝置更新規則的唯一識別碼。裝置更新規則的 Identity 可分為兩個部分：接受裝置更新規則指派的服務 (如 service:WebServer:atl-cs-001.litwareinc.com) 和全域唯一識別碼 (GUID)。因此，針對 Redmond 網站設定之裝置更新規則的 Identity 會和以下範例相似：service:WebServer:atl-cs-001.litwareinc.com /d5ce3c10-2588-420a-82ac-dc2d9b1222ff9。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule 物件。**Approve-CsDeviceUpdateRule** Cmdlet 接受裝置更新規則物件管線傳送的執行個體。

## 傳回類型

無。反之，**Approve-CsDeviceUpdateRule** Cmdlet 會核准 Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsDeviceUpdateRule](get-csdeviceupdaterule.md)  
[Remove-CsDeviceUpdateRule](remove-csdeviceupdaterule.md)  
[Reset-CsDeviceUpdateRule](reset-csdeviceupdaterule.md)  
[Restore-CsDeviceUpdateRule](restore-csdeviceupdaterule.md)

