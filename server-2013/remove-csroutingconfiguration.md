---
title: Remove-CsRoutingConfiguration
TOCTitle: Remove-CsRoutingConfiguration
ms:assetid: 80239fed-89ef-4ccc-be9b-d9149182d0c3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398643(v=OCS.15)
ms:contentKeyID: 49291477
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsRoutingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

將路由組態重設為預設值。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsRoutingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例 (只) 會將 Global 路由組態重設為預設值。此動作會刪除所有已定義的語音路由，所以我們會加上 Confirm 參數來接收提示，在移除之前詢問是否真的想要執行此動作。

    Remove-CsRoutingConfiguration -Identity Global -Confirm

## 詳細描述

語音路由所包含的指示會指示 Lync Server 如何將 Enterprise Voice 使用者的來電轉接至公用交換電話網路 (PSTN) 或專用交換機 (PBX) 上的電話號碼。此 Cmdlet 會移除全域 (且只有) 路由組態 (即容納所有針對 Lync Server 部署所定義之所有語音路由的容器)。「移除」路由組態並非實際將其移除，Global (且只有) 執行個體仍然存在，但會將語音路由清單設定為預設值。

警告：移除路由組態 (換言之，將語音路由清單設定為預設值) 會刪除 Lync Server 部署的所有已定義語音路由，並取代為具有預設值的單一路由。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsRoutingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsRoutingConfiguration"}

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
<td><p>要移除之路由組態的範圍。這個值必須是 Global。</p></td>
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
<td><p>隱藏變更前所顯示的確認提示。</p></td>
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

Microsoft.Rtc.Management.Policy.Voice.PSTNRoutingSettings 物件。接受路由組態物件管線傳送的輸入。

## 傳回類型

此 Cmdlet 會移除 (重設) Microsoft.Rtc.Management.Policy.Voice.PSTNRoutingSettings 類型的物件。

## 請參閱

#### 其他資源

[New-CsRoutingConfiguration](new-csroutingconfiguration.md)  
[Set-CsRoutingConfiguration](set-csroutingconfiguration.md)  
[Get-CsRoutingConfiguration](get-csroutingconfiguration.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

