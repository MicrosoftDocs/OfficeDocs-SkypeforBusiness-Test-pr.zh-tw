---
title: New-CsNetworkInterRegionRoute
TOCTitle: New-CsNetworkInterRegionRoute
ms:assetid: 97deeba5-b49f-4078-9843-fee7b2d1e72e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398779(v=OCS.15)
ms:contentKeyID: 49291738
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkInterRegionRoute

 

_**上次修改主題的時間：** 2015-03-09_

建立新的路由，以連接通話許可控制 (CAC) 組態內的網路區域。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsNetworkInterRegionRoute -InterNetworkRegionRouteID <String> <COMMON PARAMETERS>

    New-CsNetworkInterRegionRoute -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -NetworkRegionID1 <String> -NetworkRegionID2 <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-NetworkRegionLinkIDs <String>] [-NetworkRegionLinks <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會在 NorthAmerica 區域與 APAC 區域之間建立新的網路區域路由。我們會給新路由指定 NA\_APAC\_Route 這個 Identity (此值會自動指派做為 InterNetworkRegionRouteID)。要連接的區域是 NorthAmerica (會做為值來傳遞給 NetworkRegionID1) 和 APAC (會做為值來傳遞給 NetworkRegionID2)。在此範例中，我們假設沒有區域連結是設定為直接將 NorthAmerica 連結至 APAC。但有從 NorthAmerica 到 EMEA (NA\_EMEA) 的連結，以及從 EMEA 到 APAC (EMEA\_APAC) 的連結。我們會使用這兩個連結 (以逗號分隔) 做為 NetworkRegionLinkIDs 參數的值。這會建立從 NorthAmerica 出發、路經 EMEA 再到 APAC 的連接，並對與這些連結相關聯的音訊及視訊連線套用任何頻寬限制。

    New-CsNetworkInterRegionRoute -Identity NA_APAC_Route -NetworkRegionID1 NorthAmerica -NetworkRegionID2 APAC -NetworkRegionLinkIDs "NA_EMEA,EMEA_APAC"

## 詳細描述

CAC 組態內的每個地區都必須有辦法存取其他每個地區。地區連結會設定地區間連線的頻寬限制，也代表實體連結，而路由會決定從甲地連線到乙地時要採取的連結路徑。此 Cmdlet 會建立該路由關聯。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsNetworkInterRegionRoute** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkInterRegionRoute"}

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
<td><p>新建網路區域路由的唯一識別碼。由於網路地區路由只建立於全域範圍，因此此識別碼不需要指定範圍，而是包含一個字串，代表該路由的唯一識別名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>InterNetworkRegionRouteID</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>這個值與 Identity 相同。您不能同時指定 Identity 和 InterNetworkRegionRouteID；針對其中一項輸入的值會自動套用到這兩項。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此路由所連接之兩個區域其中一個的 Identity (NetworkRegionID)。傳給此參數的值必須是與 NetworkRegionID2 參數的值不同的區域 (換言之，您無法將區域路由給它自己)。此外，NetworkRegionID1 與 NetworkRegionID2 的結合必須是唯一的 (例如，您無法定義兩個連接 NorthAmerica 和 EMEA 的路由)。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此路由所連接之兩個區域其中一個的 Identity (NetworkRegionID)。傳給此參數的值必須是與 NetworkRegionID1 參數的值不同的區域 (換言之，您無法將區域路由給它自己)。此外，NetworkRegionID1 與 NetworkRegionID2 的結合必須是唯一的 (例如，您無法定義兩個連接 NorthAmerica 和 EMEA 的路由)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinkIDs</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您以逗號分隔值字串指定此路由的所有連結。這些值是區域連結的 Identity (NetworkRegionLinkIDs)。如果您同時輸入 NetworkRegionLinkIDs 與 NetworkRegionLinks 的值，將忽略 NetworkRegionLinkIDs。此參數提供一個便利方法，讓您不需要建構清單物件即可指定連結清單，並將它傳給 NetworkRegionLinks 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionLinks</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>物件清單，包含套用於此路由之各區域連結的 Identity (NetworkRegionLinkIDs)。對於此 Cmdlet 而言，此參數與 NetworkRegionLinkIDs 參數唯一的不同就是輸入多個連結時的格式。NetworkRegionLinkIDs 參數是要隨此 Cmdlet 定義初始清單時的建議方法。</p></td>
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

無。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsNetworkInterRegionRoute](remove-csnetworkinterregionroute.md)  
[Set-CsNetworkInterRegionRoute](set-csnetworkinterregionroute.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)

