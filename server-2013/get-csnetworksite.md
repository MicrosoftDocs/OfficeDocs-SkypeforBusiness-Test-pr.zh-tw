---
title: Get-CsNetworkSite
TOCTitle: Get-CsNetworkSite
ms:assetid: 9627869d-101f-4668-bee2-01fce1d84cbd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398766(v=OCS.15)
ms:contentKeyID: 49291744
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkSite

 

_**上次修改主題的時間：** 2015-03-09_

擷取一或多個為通話許可控制 (CAC) 或增強型 9-1-1 (E9-1-1) 所定義的網站。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsNetworkSite [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkSite [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

呼叫不含任何參數的 **Get-CsNetworkSite** Cmdlet 會傳回 Lync Server 部署內所有針對 CAC 或 E9-1-1 設定的網站。

    Get-CsNetworkSite

## 範例 2

此命令會擷取其 Identity (依定義也是 NetworkSiteID) 為 Redmond 的網站。

    Get-CsNetworkSite -Identity Redmond

## 範例 3

範例 3 的命令會呼叫 **Get-CsNetworkSite** Cmdlet 並搭配 Filter 參數。Filter 參數的值為 NA\*，表示此命令將擷取 Identity 以 NA 字串開頭且後面接著任意字元數量的所有網站。這將傳回如 NARedmond、NAVancouver 和 NAChicago 之類的網站。

    Get-CsNetworkSite -Filter NA*

## 範例 4

範例 4 會使用兩個 Cmdlet (**Get-CsNetworkSite** Cmdlet 和 **Where-Object** Cmdlet) 擷取所有隸屬於 NorthAmerica 區域的網站。此命令會先呼叫不含任何參數的 **Get-CsNetworkSite** Cmdlet 來擷取所有網站。然後，將此網站集合管線傳送至 **Where-Object** Cmdlet，這會篩選集合，尋找集合中所有 NetworkRegionID 屬性等於 (-eq) NorthAmerica 的網站。

    Get-CsNetworkSite | Where-Object {$_.NetworkRegionID -eq "NorthAmerica"}

## 詳細描述

網站是指在 CAC 或 E9-1-1 部署的每一個區域內設定的辦公室或位置。此 Cmdlet 會擷取一或多個現有網站的設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsNetworkSite** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkSite"}

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
<td><p>萬用字元字串，可讓您將網站 Identity 比對 Filter 值來擷取多個網站。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>您要擷取之網站的唯一識別碼。只會在全域範圍建立網站，所以您不必指定範圍。而只需要指定網站 ID (請注意，此值與網站的 NetworkSiteID 值相同)。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取網站資訊，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

擷取 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkSite](new-csnetworksite.md)  
[Remove-CsNetworkSite](remove-csnetworksite.md)  
[Set-CsNetworkSite](set-csnetworksite.md)

