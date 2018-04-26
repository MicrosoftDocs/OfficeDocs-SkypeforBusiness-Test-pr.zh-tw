---
title: Set-CsNetworkSubnet
TOCTitle: Set-CsNetworkSubnet
ms:assetid: 9e85cdbb-b5fb-48d6-8f95-6e7cba9d9597
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412739(v=OCS.15)
ms:contentKeyID: 49291819
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkSubnet

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的網路子網路。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsNetworkSubnet [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkSubnet [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-MaskBits <Int32>] [-NetworkSiteID <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會修改 Identity (子網路 ID) 為 172.11.15.0 的子網路。此子網路會修改為新的 MaskBits 值 (25) 以及新的 NetworkSiteID (Chicago)。

    Set-CsNetworkSubnet -Identity 172.11.15.0 -MaskBits 25 -NetworkSiteID Chicago

## 範例 2

範例 2 會將 Vancouver 網站上的所有子網路移至 Chicago 網站。為達成此目的，我們會先呼叫 **Get-CsNetworkSubnet** Cmdlet，以擷取 Lync Server 部署中定義之所有子網路的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會將該集合縮小到只含 NetworkSiteID 等於 (-eq) Vancouver 的子網路。至此這個集合只包含與 Vancouver 網站相關聯的子網路，我們再將該集合管線傳送到 **Set-CsNetworkSubnet** Cmdlet。然後為 **Set-CsNetworkSubnet** Cmdlet 提供 NetworkSiteID 參數。接著再將 Chicago 的值傳遞給參數，指示 **Set-CsNetworkSubnet** Cmdlet 將集合中每個成員的網站識別碼變更為 Chicago。

    Get-CsNetworkSubnet | Where-Object {$_.NetworkSiteID -eq "Vancouver"} | Set-CsNetworkSubnet -NetworkSiteID Chicago

## 詳細描述

為了判斷屬於此子網路的主機地理位置，每一個子網路都必須與網站相關聯。使用此 Cmdlet 可修改相關聯的網站、變更子網路的描述，或是修改子網路的遮罩位元。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsNetworkSubnet** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkSubnet"}

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
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>要修改之子網路的描述。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>要修改之子網路的唯一子網路 ID。此值必須是 IP 位址 (例如 174.11.12.0) 或以 http: 或 https: 開頭的 URL。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>子網路類型</p></td>
<td><p>要修改之網路子網路物件的參考。此物件的類型必須是 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType，這可透過呼叫 <strong>Get-CsNetworkSubnet</strong> Cmdlet 來擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>MaskBits</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>要套用至子網路的位元遮罩。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>要套用此子網路之網站的網站識別碼。您可以呼叫 <strong>Get-CsNetworkSite</strong> Cmdlet 來擷取部署的網站識別碼。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType 物件。接受網路子網路物件的管線傳送資料。

## 傳回類型

此 Cmdlet 不會傳回值，而會修改 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkSubnet](new-csnetworksubnet.md)  
[Remove-CsNetworkSubnet](remove-csnetworksubnet.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)

