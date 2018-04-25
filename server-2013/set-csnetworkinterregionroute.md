---
title: Set-CsNetworkInterRegionRoute
TOCTitle: Set-CsNetworkInterRegionRoute
ms:assetid: 5d9da3c0-56fc-401d-baf3-ed6c0f50f53d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398410(v=OCS.15)
ms:contentKeyID: 49291057
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkInterRegionRoute

 

_**上次修改主題的時間：** 2015-03-09_

修改通話許可控制 (CAC) 組態中目前用以連接網路區域的路由。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsNetworkInterRegionRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkInterRegionRoute [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkRegionID1 <String>] [-NetworkRegionID2 <String>] [-NetworkRegionLinkIDs <String>] [-NetworkRegionLinks <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會透過變更將周遊路由的區域連結來修改路由 NA\_APAC\_Route。NetworkRegionLinkIDs 參數會搭配值 “NA\_SA,SA\_APAC” 使用，以該字串中指定的兩個連結來取代任何現有的連結。

    Set-CsNetworkInterRegionRoute -Identity NA_APAC_Route -NetworkRegionLinkIDs "NA_SA,SA_APAC"

## 範例 2

與範例 1 類似，範例 2 會修改 NA\_APAC\_Route 路由中的連結。不過，在此範例中不是使用 NetworkRegionLinkIDs 參數來取代該路由的所有連結，而是使用 NetworkRegionLinks 參數將連結新增至該路由中已存在的連結清單。在此範例中，SA\_EMEA 連結會新增至該路由。語法 @{add=\<link\>} 會將一個元素新增至連結清單。您也可以使用語法 @{replace=\<link\>}，以 \<link\> 指定的連結取代所有現有的連結 (基本上與使用 NetworkRegionLinkIDs 的行為相同)，或是使用語法 @{remove=\<link\>} 從清單中移除連結。

    Set-CsNetworkInterRegionRoute -Identity NA_APAC_Route -NetworkRegionLinks @{add="SA_EMEA"}

## 範例 3

範例 3 會修改名稱為 NA\_Route5 的路由。此範例會變更組成此路由的其中一個區域。NetworkRegionID2 參數是用來指定新區域，而 NetworkRegionLinkIDs 參數則是用來建立新的連結清單，以連接此路由的區域。

    Set-CsNetworkInterRegionRoute -Identity NA_Route5 -NetworkRegionID2 SouthAmerica -NetworkRegionLinkIDs "NA_SA,SA_APAC"

## 詳細描述

CAC 組態中的每個區域都必須有存取其他每個區域的特定方法。地區連結會設定地區間連線的頻寬限制，也代表實體連結，而路由會決定從甲地連線到乙地時要採取的連結路徑。此 Cmdlet 會修改該路由關聯。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsNetworkInterRegionRoute** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkInterRegionRoute"}

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
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>您要修改之網路區域路由的唯一識別碼。網路區域路由只會在全域範圍建立，因此，這個識別碼不需要指定範圍。但是，它包含識別該路由之唯一名稱的字串。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>內部網路區域路由類型</p></td>
<td><p>現有區域路由的物件參考。這個物件必須屬於 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType 類型 (可藉由呼叫 <strong>Get-CsNetworkInterRegionRoute</strong> Cmdlet 擷取)。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>透過此路由連線的兩個區域中，其中一個區域的 Identity (NetworkRegionID)。傳遞到此參數的值必須與 NetworkRegionID2 參數的值是不同的區域 (也就是說，您無法將區域路由傳送至本身)。此外，NetworkRegionID1 和 NetworkRegionID2 的組合必須是唯一的 (例如，您無法定義連接 NorthAmerica 和 EMEA 的兩個路由)。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>透過此路由連線的兩個區域中，其中一個區域的 Identity (NetworkRegionID)。傳遞到此參數的值必須與 NetworkRegionID1 參數的值是不同的區域 (也就是說，您無法將區域路由傳送至本身)。此外，NetworkRegionID1 和 NetworkRegionID2 的組合必須是唯一的 (例如，您無法定義連接 NorthAmerica 和 EMEA 的兩個路由)。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionLinkIDs</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>可讓您將此路由的所有連結指定為逗號分隔值的字串。這些值是區域連結的 Identity (NetworkRegionLinkIDs)。如果您同時輸入 NetworkRegionLinkIDs 與 NetworkRegionLinks 的值，將忽略 NetworkRegionLinkIDs。使用此參數修改的任何連結都會取代路由中的所有現有連結。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinks</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>包含套用到此路由之區域連結 Identity (NetworkRegionLinkIDs) 的清單物件。對於此 Cmdlet，此參數與 NetworkRegionLinkIDs 不同之處為除了可讓您取代此路由的所有現有連結外，還可以新增或移除個別連結。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType 物件。接受管線傳送的網路區間路由物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會修改 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Remove-CsNetworkInterRegionRoute](remove-csnetworkinterregionroute.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)

