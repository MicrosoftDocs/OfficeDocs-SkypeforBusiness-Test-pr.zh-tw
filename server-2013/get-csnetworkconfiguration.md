---
title: Get-CsNetworkConfiguration
TOCTitle: Get-CsNetworkConfiguration
ms:assetid: 08bc8eca-b244-4d5e-b089-1cc95605ba14
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398140(v=OCS.15)
ms:contentKeyID: 49290010
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

擷取通話許可控制 (CAC)、增強型 9-1-1 (E9-1-1) 及媒體旁路的全域設定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsNetworkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

此範例會擷取網路組態設定。這些設定只會在全域範圍定義，因此只會傳回一個項目。

    Get-CsNetworkConfiguration

## 範例 2

只有一組媒體旁路設定存在 (全域套用)。這些設定會儲存為整體網路組態的一部分。此命令會先呼叫 **Get-CsNetworkConfiguration** Cmdlet 來擷取該組態，然後再擷取該組態的 MediaBypassSettings 屬性。

    (Get-CsNetworkConfiguration).MediaBypassSettings

## 詳細描述

網路組態物件包含 Lync Server 部署中針對媒體略過和整個 CAC 組態的所有全域設定，包括是否已啟用該組態。您可以使用此 Cmdlet 擷取這些組態和設定。不過，除了 EnableBandwidthPolicyCheck 和 MediaBypassSettings 之外，建議您在擷取 CAC 組態設定時使用物件類型專用的 Cmdlet。例如，若要擷取網路區域，通常呼叫 **Get-CsNetworkRegion** Cmdlet 會比呼叫 **Get-CsNetworkConfiguration** Cmdlet，然後擷取該組態的 NetworkRegions 屬性更容易。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsNetworkConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkConfiguration"}

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
<td><p>因為只會有一個網路組態，因此此 Cmdlet 不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>這一律為 Global。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取網路組態，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Get-CsNetworkConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Remove-CsNetworkConfiguration](remove-csnetworkconfiguration.md)  
[Set-CsNetworkConfiguration](set-csnetworkconfiguration.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

