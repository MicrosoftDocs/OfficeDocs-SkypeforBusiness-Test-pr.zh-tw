---
title: 在 Lync Server 2013 中部署網路區域、網站和子網路
TOCTitle: 在 Lync Server 2013 中部署網路區域、網站和子網路
ms:assetid: c4b75601-3538-4d07-8d23-1ad90459ae48
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994067(v=OCS.15)
ms:contentKeyID: 52056220
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中部署網路區域、網站和子網路

 

_**上次修改主題的時間：** 2015-03-09_

部署企業語音後，您需要設定：

  - 網路區域

  - 網站

  - 子網路

## 定義網路區域

使用 Lync ServerWindows PowerShell 命令 New-CsNetworkRegion 或 Lync Server 控制台 定義網路區域。

    New-CsNetworkRegion -NetworkRegionID <region ID> -CentralSite <site ID>

如需詳細資訊，請參閱＜[New-CsNetworkRegion](new-csnetworkregion.md)＞。

就此範例而言，下列 Windows PowerShell 命令說明了此案例中定義的網路區域 1 (India)。

    New-CsNetworkRegion -NetworkRegionID "India" -CentralSite "India Central Site"


## 定義網站

使用 Lync ServerWindows PowerShell 命令 New-CsNetworkSite 或 Lync Server 控制台 定義網站。

    New-CsNetworkSite -NetworkSiteID <site ID> -NetworkRegionID <region ID>

如需詳細資訊，請參閱＜[New-CsNetworkSite](new-csnetworksite.md)＞。

就此範例而言，下表和 Lync ServerWindows PowerShell 命令說明了此案例中定義的網站。表中只包括位置基礎路由的特有設定，做為說明之用。

    New-CsNetworkSite -NetworkSiteID "Delhi" -NetworkRegionID "India"
    New-CsNetworkSite -NetworkSiteID "Hyderabad" -NetworkRegionID "India"


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>網站 1 (Delhi)</th>
<th>網站 2 (Hyderabad)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>網站 ID</p></td>
<td><p>網站 1 (Delhi)</p></td>
<td><p>網站 2 (Hyderabad)</p></td>
</tr>
<tr class="even">
<td><p>區域 ID</p></td>
<td><p>區域 1 (India)</p></td>
<td><p>區域 1 (India)</p></td>
</tr>
</tbody>
</table>



## 定義子網路

使用 Lync ServerWindows PowerShell 命令 New-CsNetworkSubnet 或 Lync Server 控制台 定義子網路，並將子網路指派給網站。

    New-CsNetworkSubnet -SubnetID <Subnet IP address> -MaskBits <Subnet bitmask> -NetworkSiteID <site ID>

如需詳細資訊，請參閱＜[New-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkSubnet)＞。

就此範例而言，下表和 Windows PowerShell 命令說明有關將子網路指派給此案例中定義之網站 (Delhi 與 Hyderabad)。表中只包括位置基礎路由的特有設定，做為說明之用。

    New-CsNetworkSubnet -SubnetID "192.168.0.0" -MaskBits "24" -NetworkSiteID "Delhi"
    New-CsNetworkSubnet -SubnetID "192.168.1.0" -MaskBits "24" -NetworkSiteID "Hyderabad"


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>網站 1 (Delhi)</th>
<th>網站 2 (Hyderabad)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>子網路 ID</p></td>
<td><p>192.168.0.0</p></td>
<td><p>192.168.1.0</p></td>
</tr>
<tr class="even">
<td><p>遮罩</p></td>
<td><p>24</p></td>
<td><p>24</p></td>
</tr>
<tr class="odd">
<td><p>網站 ID</p></td>
<td><p>網站 1 (Delhi)</p></td>
<td><p>網站 2 (Hyderabad)</p></td>
</tr>
</tbody>
</table>



## 請參閱

#### 其他資源

[在 Lync Server 2013 中設定位置基礎路由](lync-server-2013-configuring-location-based-routing.md)

