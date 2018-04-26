---
title: Remove-CsDeviceUpdateRule
TOCTitle: Remove-CsDeviceUpdateRule
ms:assetid: 42b0bcd5-d567-4867-841e-0d35ac05c09f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425930(v=OCS.15)
ms:contentKeyID: 49290738
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDeviceUpdateRule

 

_**上次修改主題的時間：** 2015-03-09_

移除設定供組織使用的裝置更新規則。裝置更新規則可用於關聯韌體更新與執行 Lync Phone Edition 的裝置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsDeviceUpdateRule -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會刪除 Identity 為 service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9 的裝置更新規則。刪除規則之後，將無法再使用對應的韌體更新。

    Remove-CsDeviceUpdateRule -Identity service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9

## 範例 2

範例 2 所示的命令會移除已設為在組織中使用的所有裝置更新規則。為達成此目的，可以呼叫 **Get-CsDeviceUpdateRule** Cmdlet (不使用任何參數) 傳回目前所使用中之所有裝置更新規則的集合。然後，此集合會管線傳送到 **Remove-CsDeviceUpdateRule**，以刪除集合中的每一個規則。

    Get-CsDeviceUpdateRule | Remove-CsDeviceUpdateRule

## 範例 3

範例 3 會移除匯入服務 WebServer:atl-cs-001.litwareinc.com 的所有裝置更新規則。為達成此目的，命令會先使用 **Get-CsDeviceUpdateRule** 和 Filter 參數，擷取 Identity 開頭為字串值 "service:WebServer:atl-cs-001.litwareinc.com " 的所有裝置更新規則。然後，此集合會管線傳送到 **Remove-CsDeviceUpdateRule** Cmdlet，以刪除該集合中的每一個規則。

    Get-CsDeviceUpdateRule -Filter service:WebServer:atl-cs-001.litwareinc.com* | Remove-CsDeviceUpdateRule

## 範例 4

範例 4 會刪除 Brand 等於 "LG-Nortel" 的所有裝置更新規則。為達此目的，此 Cmdlet 會會先呼叫不含任何參數的 **Get-CsDeviceUpdateRule** Cmdlet，以擷取組織正在使用之所有裝置更新規則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 Brand 等於 "LG-Nortel" 的規則。接著會將篩選後的集合傳送到 **Remove-CsDeviceUpdateRule** Cmdlet，以移除集合中的每個規則。

    Get-CsDeviceUpdateRule | Where-Object {$_.Brand -eq "LG-Nortel"} | Remove-CsDeviceUpdateRule

## 詳細描述

Lync Server 使用裝置更新規則來提供韌體更新給執行 Lync Phone Edition 的裝置。系統管理員會定期將一組裝置更新規則上傳到 Lync Server；那些規則經過測試與核准後，裝置與系統連線時會自動下載那些規則並套用到裝置。根據預設，裝置每次開啟並連線到 Lync Server 時，都會檢查新的更新規則。在最初登入之後，裝置每隔 24 小時也會檢查一次更新。

系統管理員無法建立他們自己的裝置更新規則；更新規則只能透過下載及匯入來自 Microsoft 網站的規則集而建立。也就是說，隨著時間推移，您很可能收集了已過期或組織中不再使用的規則 (例如，如果您的組織不再使用 LG-Nortel 電話，就不再需要那些裝置的韌體更新)。雖然這些不需要的規則不會造成任何問題，但是會使管理變得複雜：執行 **Get-CsDeviceUpdateRule** Cmdlet 以傳回所有裝置更新規則的集合時，卻發現大多數規則不適用於您組織，這是很令人困擾的。為了協助減少這樣的困擾，可以使用 **Remove-CsDeviceUpdateRule** Cmdlet 以移除已匯入供使用的所有裝置更新規則 (或規則集)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsDeviceUpdateRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDeviceUpdateRule"}

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
<td><p>裝置更新規則的唯一識別碼。裝置更新規則的 Identity 包含兩個部分：已套用規則的服務範圍 (例如 service:WebServer:atl-cs-001.litwareinc.com) 和預先指派給規則的全域唯一識別碼 (GUID) (例如 d5ce3c10-2588-420a-82ac-dc2d9b1222ff9)。在此基礎上，指定裝置更新規則的 Identity 的外觀類似如下：&quot;service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9 &quot;。</p>
<p>指定 Identity 時不允許使用萬元字元。</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule 物件。**Remove-CsDeviceUpdateRule** Cmdlet 接受管線傳送的裝置更新規則物件執行個體。

## 傳回類型

**Remove-CsDeviceUpdateRule** Cmdlet 不會傳回值或物件，而會刪除 Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.Rule 物件的執行個體。

## 請參閱

#### 其他資源

[Approve-CsDeviceUpdateRule](approve-csdeviceupdaterule.md)  
[Get-CsDeviceUpdateRule](get-csdeviceupdaterule.md)  
[Reset-CsDeviceUpdateRule](reset-csdeviceupdaterule.md)  
[Restore-CsDeviceUpdateRule](restore-csdeviceupdaterule.md)

