---
title: Get-CsNetworkSubnet
TOCTitle: Get-CsNetworkSubnet
ms:assetid: ad74155a-8d83-42f6-bb1e-8bfc7d57d5b0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412825(v=OCS.15)
ms:contentKeyID: 49292004
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkSubnet

 

_**上次修改主題的時間：** 2015-03-09_

擷取一或多個網路子網路的資訊。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsNetworkSubnet [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkSubnet [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

此範例擷取 Lync Server 部署內的所有子網路。

    Get-CsNetworkSubnet

## 範例 2

此範例會擷取 Identity (子網路 ID) 為 172.11.15.0 的子網路的所有資訊。

    Get-CsNetworkSubnet -Identity 172.11.15.0

## 範例 3

此範例會擷取 Identity 以 172.11. 開頭的所有子網路。

    Get-CsNetworkSubnet -Filter 172.11.*

## 範例 4

範例 4 會擷取所有與 Vancouver 網站相關聯的子網路。我們會先呼叫不含任何參數的 **Get-CsNetworkSubnet** Cmdlet，如同在範例 2 中所見，這會擷取所有定義的子網路。接著將此子網路集合管線傳送到 **Where-Object** Cmdlet。 **Where-Object** Cmdlet 採用該集合並縮小範圍至只有 NetworkSiteID 等於 (-eq) Vancouver 的子網路。

    Get-CsNetworkSubnet | Where-Object {$_.NetworkSiteID -eq "Vancouver"}

## 詳細描述

為了判斷屬於此子網路的主機地理位置，每一個子網路都必須與網站相關聯。使用此 Cmdlet 擷取子網路的資訊，包括 Identity (子網路 ID)、遮罩位元數、關聯的網站及子網路的描述。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsNetworkSubnet** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkSubnet"}

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>使用此參數根據 Identity 對所有子網路執行萬用字元搜尋。例如，篩選值 172.11.* 將擷取所有 Identity 以 172.11 開頭的子網路 (如 172.11.10.0、172.11.25.0 等)。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>您要擷取的子網路的唯一子網路 ID。這個值為 IP 位址 (例如 174.11.12.0)。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區本機複本擷取網路子網路資訊，而不從 中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

傳回一或多個 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkSubnet](new-csnetworksubnet.md)  
[Remove-CsNetworkSubnet](remove-csnetworksubnet.md)  
[Set-CsNetworkSubnet](set-csnetworksubnet.md)

