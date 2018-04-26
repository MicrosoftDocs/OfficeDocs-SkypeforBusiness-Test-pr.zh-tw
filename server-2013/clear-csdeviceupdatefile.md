---
title: Clear-CsDeviceUpdateFile
TOCTitle: Clear-CsDeviceUpdateFile
ms:assetid: 34c5bb61-fcba-4e93-bb21-83b9611f3045
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425835(v=OCS.15)
ms:contentKeyID: 49290552
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Clear-CsDeviceUpdateFile

 

_**上次修改主題的時間：** 2015-03-09_

刪除遭到拒絕並與裝置無關的裝置更新檔案。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Clear-CsDeviceUpdateFile -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會從 WebServer:atl-cs-001.litwareinc.com 服務刪除不再與裝置相關聯的所有裝置更新檔。

    Clear-CsDeviceUpdateFile -Identity "service:WebServer:atl-cs-001.litwareinc.com"

## 詳細描述

每次將新裝置更新上傳至系統時，就會建立對應的裝置更新規則。根據預設，這些新裝置更新規則會被指派為「擱置」狀態；也就是說，您可以將規則下載並安裝在測試裝置上，但無法下載並安裝在生產裝置上。如此可讓您在將更新提供給使用者之前先進行測試。如果測試成功，您可以執行 **Approve-CsDeviceUpdateRule** Cmdlet，以便將這些裝置更新提供給使用者。

如果測試不成功，則您可以使用 **Reset-CsDeviceUpdateRule** Cmdlet 或 **Restore-CsDeviceUpdateRule** Cmdlet 來拒絕更新。執行這些 Cmdlet 時，裝置更新會與其裝置更新規則解除關聯。這時候系統管理員就可以使用 **Clear-CsDeviceUpdateFile** Cmdlet，從伺服器移除已解除關聯的更新。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Clear-CsDeviceUpdateFile** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Clear-CsDeviceUpdateFile"}

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
<td><p>裝載裝置更新檔之服務的唯一識別碼。例如，此語法會從 atl-cs-001.litwareinc.com 集區的 Web 服務 服務清除裝置更新檔：-Identity &quot;service:WebServer:atl-cs-001.litwareinc.com&quot;。</p></td>
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

無。**Clear-CsDeviceUpdateFile** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。**Clear-CsDeviceUpdateFile** Cmdlet 不會傳回任何值。

## 請參閱

#### 其他資源

[Clear-CsDeviceUpdateLog](clear-csdeviceupdatelog.md)  
[Get-CsDeviceUpdateConfiguration](get-csdeviceupdateconfiguration.md)

