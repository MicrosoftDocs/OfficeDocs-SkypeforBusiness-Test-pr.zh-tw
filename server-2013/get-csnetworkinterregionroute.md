---
title: Get-CsNetworkInterRegionRoute
TOCTitle: Get-CsNetworkInterRegionRoute
ms:assetid: 31c38d92-1cef-40fe-bd04-26e5b373703e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425817(v=OCS.15)
ms:contentKeyID: 49290512
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterRegionRoute

 

_**上次修改主題的時間：** 2015-03-09_

擷取通話許可控制 (CAC) 組態中用於連線網路區域的一或多個路由。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsNetworkInterRegionRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterRegionRoute [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會擷取 Identity 為 NA\_APAC\_Route 的路由。

    Get-CsNetworkInterRegionRoute -Identity NA_APAC_Route

## 範例 2

在範例 2 中，我們使用 Filter 參數來擷取 Identity 中任何位置包含字串 APAC 的所有路由。

    Get-CsNetworkInterRegionRoute -Filter *APAC*

## 範例 3

此範例會擷取使用網路區域連結 NA\_EMEA 的所有區域路由。此命令會先呼叫不含任何參數的 **Get-CsNetworkInterRegionRoute** Cmdlet，以擷取 CAC 組態中所定義的所有路由。然後再將該路由集合管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會取得該集合並擷取集合的 NetworkRegionLinks 清單中擁有 NA\_EMEA 值的所有項目。

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionLinks -eq "NA_EMEA"}

## 範例 4

範例 4 會擷取包含 NorthAmerica 區域的所有區域路由。命令的第一個部分是對 **Get-CsNetworkInterRegionRoute** Cmdlet 的呼叫。這個以不含任何參數呼叫的 Cmdlet 會擷取所有區域路由。接著，將此路由集合傳送至 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會將集合縮小到只含有定義了 NorthAmerica 做為路由途中其中一個地區的路由。作法是，檢查路由的 NetworkRegionID1 值是否等於 (-eq) NorthAmerica，或者其 (-or) NetworkRegionID2 值等於 NorthAmerica。

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionID1 -eq "NorthAmerica" -or $_.NetworkRegionID2 -eq "NorthAmerica"}

## 詳細描述

CAC 組態中的每個區域都必須有存取其他每個區域的特定方法。地區連結會設定地區間連線的頻寬限制，也代表實體連結，而路由會決定從甲地連線到乙地時要採取的連結路徑。此 Cmdlet 會擷取這些路由關聯的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsNetworkInterRegionRoute** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterRegionRoute"}

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
<td><p>字串，可讓您根據 Identity 值與當做值傳遞到此參數之萬用字元字串之間的比對來擷取路由。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>您要擷取之網路區域路由的唯一識別碼。網路區域路由只會在全域範圍建立，因此，這個識別碼不需要指定範圍。而是包含一個字串，代表特定路由的唯一識別名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取網路區間路由資訊，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

此 Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType 類型的一或多個物件。

## 請參閱

#### 其他資源

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Remove-CsNetworkInterRegionRoute](remove-csnetworkinterregionroute.md)  
[Set-CsNetworkInterRegionRoute](set-csnetworkinterregionroute.md)

