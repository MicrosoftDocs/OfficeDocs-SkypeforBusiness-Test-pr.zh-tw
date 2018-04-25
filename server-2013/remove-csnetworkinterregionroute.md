---
title: Remove-CsNetworkInterRegionRoute
TOCTitle: Remove-CsNetworkInterRegionRoute
ms:assetid: 91948c03-2bcb-4e25-b0b6-23827e85bbb3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398743(v=OCS.15)
ms:contentKeyID: 49291672
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkInterRegionRoute

 

_**上次修改主題的時間：** 2015-03-09_

移除連接通話許可控制 (CAC) 組態內之網路地區的路由。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsNetworkInterRegionRoute -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會移除其 Identity 為 NA\_APAC\_Route 的路由。

    Remove-CsNetworkInterRegionRoute -Identity NA_APAC_Route

## 範例 2

範例 2 會移除所有包含 NorthAmerica 地區的地區路由。命令的第一個部分是呼叫 **Get-CsNetworkInterRegionRoute** Cmdlet。呼叫此 Cmdlet (不含任何參數)，將會擷取所有地區路由。接著，將此路由集合管線傳送至 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會將集合縮小到只含 NorthAmerica 定義為路由中其中一個地區的路由。作法是檢查路由的 NetworkRegionID1 值是否等於 (-eq) NorthAmerica 或 (-or) NetworkRegionID2 值是否等於 NorthAmerica。一旦集合只有包含 NorthAmerica 地區的路由後，我們會將該集合管線傳送至 **Remove-CsNetworkInterRegionRoute** Cmdlet，以移除其中每個路由。

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionID1 -eq "NorthAmerica" -or $_.NetworkRegionID2 -eq "NorthAmerica"} | Remove-CsNetworkInterRegionRoute

## 詳細描述

CAC 組態內的每個地區都必須有辦法存取其他每個地區。地區連結會設定地區間連線的頻寬限制，也代表實體連結，而路由會決定從甲地連線到乙地時要採取的連結路徑。此 Cmdlet 會移除這其中一個路由關聯。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsNetworkInterRegionRoute** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkInterRegionRoute"}

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
<td><p>您要移除之網路地區路由的唯一識別碼。由於網路地區路由只建立於全域範圍，因此此識別碼不需要指定範圍，而是包含一個字串，代表該路由的唯一識別名稱。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType 物件。接受管線傳送的網路區域間路由物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Set-CsNetworkInterRegionRoute](set-csnetworkinterregionroute.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)

