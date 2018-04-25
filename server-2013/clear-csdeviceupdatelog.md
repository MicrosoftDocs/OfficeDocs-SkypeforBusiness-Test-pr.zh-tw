---
title: Clear-CsDeviceUpdateLog
TOCTitle: Clear-CsDeviceUpdateLog
ms:assetid: 9e549484-b79b-47ef-b83b-13a6e20b0c80
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412738(v=OCS.15)
ms:contentKeyID: 49291818
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Clear-CsDeviceUpdateLog

 

_**上次修改主題的時間：** 2015-03-09_

刪除所有長於指定天數的裝置更新 Web 服務記錄檔與稽核檔案。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Clear-CsDeviceUpdateLog -DaysBack <Int32> -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會連線至 Identity 為 "service:WebServer:atl-cs-001.litwareinc.com" 的裝置更新 Web 服務，並刪除 10 天以上的所有裝置和稽核記錄。

    Clear-CsDeviceUpdateLog -Identity "service:WebServer:atl-cs-001.litwareinc.com" -DaysBack 10

## 詳細描述

裝置更新 Web 服務會保存大量的記錄檔集合；此集合包括服務本身進行的稽核記錄，以及從用戶端裝置 (如行動電話) 上傳的記錄檔。根據裝置更新活動量以及組織中使用的用戶端裝置數目，裝置更新 Web 服務記錄檔很快就會「塞滿」您的伺服器。**Clear-CsDeviceUpdateLog** Cmdlet 可讓您減少儲存在伺服器上的記錄檔數目。您只需要執行該 Cmdlet，並指定不應刪除之檔案的保留時間上限 (天)。如此即可移除系統上長於保留時間限制的記錄檔。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Clear-CsDeviceUpdateLog** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Clear-CsDeviceUpdateLog"}

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
<td><p><em>DaysBack</em></p></td>
<td><p>必要</p></td>
<td><p>System.Int32</p></td>
<td><p>要保留之記錄檔的保留時間上限 (天)。早於使用 DaysBack 參數指定之值的所有記錄檔都會遭到刪除。例如，如果您將 DaysBack 設為 7，則七天以上的任何記錄檔將會遭到移除。</p>
<p>此參數可以設為 1 和 30 (含) 之間的任何整數值。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>主控裝置更新 Web 服務記錄檔之服務的唯一識別碼。例如，此語法會針對 atl-cs-001.litwareinc.com 集區，從 Web 服務清除裝置更新 Web 服務記錄檔：-Identity &quot;service:WebServer:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Clear-CsDeviceUpdateLog** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。**Clear-CsDeviceUpdateLog** Cmdlet 不會傳回任何值。

## 請參閱

#### 其他資源

[Clear-CsDeviceUpdateFile](clear-csdeviceupdatefile.md)  
[Get-CsDeviceUpdateConfiguration](get-csdeviceupdateconfiguration.md)

