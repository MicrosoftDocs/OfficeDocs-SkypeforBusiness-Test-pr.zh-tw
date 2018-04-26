---
title: Remove-CsNetworkRegion
TOCTitle: Remove-CsNetworkRegion
ms:assetid: 661dce40-f601-4181-b8f1-3277a76d5df4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398466(v=OCS.15)
ms:contentKeyID: 49291150
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkRegion

 

_**上次修改主題的時間：** 2015-03-09_

移除現有網路區域。網路區域代表企業網路中的網路集線器或骨幹。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsNetworkRegion -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會移除 Identity 為 NorthAmerica 的網路區域。因為識別是唯一的，所以此命令只會移除一個網路區域。

    Remove-CsNetworkRegion -Identity NorthAmerica

## 範例 2

此範例會移除與 中央網站 Redmond 相關聯的所有網路區域。命令會先呼叫不含任何參數的 **Get-CsNetworkRegion** Cmdlet，以擷取為 Lync Server 部署定義的所有網路區域集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會篩選此集合，而只傳回 CentralSite 值等於 (-eq) site:Redmond 的項目 (網路區域)。將集合縮小到只剩下所需項目之後，會將此新的集合管線傳送到 **Remove-CsNetworkRegion** Cmdlet，以移除該集合中的每個項目。

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"} | Remove-CsNetworkRegion

## 範例 3

這個範例會移除 Identity 為 NorthAmerica 的網路區域。但是如果區域與某個網站相關聯時，則無法移除該區域。所以此範例會先移除 NorthAmerica 區域與網站之間的任何關聯。

範例會先呼叫不含參數的 **Get-CsNetworkSite** Cmdlet，以擷取為 Lync Server 部署所定義的所有網路網站集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會篩選此集合，而只傳回 NetworkRegionID 值等於 (-eq) NorthAmerica 的項目 (網路網站)。將集合縮小到那些項目之後，便將這個新集合管線傳送到 **Set-CsNetworkSite** Cmdlet。針對 NetworkRegionID 為 NorthAmerica 的每個網站，我們會將 NetworkRegionID 設為 Null ($null)。這會移除該網站對區域的參考。但是，如果網站未與網站相關聯，網站便不能擁有旁路 ID。所以除了透過將 NetworkRegionID 設為 Null 來移除對區域的參考外，我們還必須將 BypassID 設為 Null 來移除旁路關聯。

第一行完成後，任何與 NorthAmerica 區域關聯的網站便不再繫結至區域或任何旁路設定。此時我們可呼叫第二行來移除網路區域。

    Get-CsNetworkSite | Where-Object {$_.NetworkRegionID -eq "NorthAmerica"} | Set-CsNetworkSite -NetworkRegionID $null -BypassID $null
    Remove-CsNetworkRegion -Identity "NorthAmerica"

## 詳細描述

網路區域會與跨多個地理區域的網路不同部分交互連線。每個網路區域都必須與中央網站產生關聯。中央網站 是執行頻寬原則服務所在的資料中心網站。使用此 Cmdlet 可移除網路區域。

請注意，如果網路區域與某個網站相關聯 (亦即有任何網站的 NetworkRegionID 等於該區域的 Identity)，則無法移除該網路區域。如果您嘗試移除與網站相關聯的區域，則會收到錯誤訊息。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsNetworkRegion** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkRegion"}

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
<td><p>要移除之網路區域的唯一識別碼。Identity 的格式是可唯一識別該區域的字串。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType 物件。接受網路區域物件的管線傳送資料。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)

