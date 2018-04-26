---
title: Remove-CsNetworkSubnet
TOCTitle: Remove-CsNetworkSubnet
ms:assetid: 251ddb5c-4837-4810-b46f-d276f9535653
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425726(v=OCS.15)
ms:contentKeyID: 49290358
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkSubnet

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的網路子網路。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsNetworkSubnet -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會移除 Identity (子網路 ID) 為 172.11.15.0. 的子網路。

    Remove-CsNetworkSubnet -Identity 172.11.15.0

## 範例 2

範例 2 會移除與 Vancouver 網站相關聯的所有子網路。為達成此目的，我們一開始先呼叫 **Get-CsNetworkSubnet** Cmdlet。這會擷取所有在 Lync Server 部署中定義的子網路集合。然後再將此子網路集合管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 採用該集合並縮小範圍至只有 NetworkSiteID 等於 (-eq) Vancouver 的子網路。現在集合只由與 Vancouver 網站相關聯的子網路組成，我們將該集合管線傳送到 **Remove-CsNetworkSubnet** Cmdlet，移除集合中的每一個項目。

    Get-CsNetworkSubnet | Where-Object {$_.NetworkSiteID -eq "Vancouver"} | Remove-CsNetworkSubnet

## 詳細描述

為了判斷屬於此子網路的主機地理位置，每一個子網路都必須與網站相關聯。使用此 Cmdlet 移除網路子網路。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsNetworkSubnet** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkSubnet"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>您要移除之子網路的唯一子網路 ID。這個值為 IP 位址 (例如 174.11.12.0)。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType 物件。接受網路子網路物件的管線傳送資料。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkSubnet](new-csnetworksubnet.md)  
[Set-CsNetworkSubnet](set-csnetworksubnet.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)

