---
title: New-CsNetworkRegionLink
TOCTitle: New-CsNetworkRegionLink
ms:assetid: 61a6a7be-8078-4d59-a78a-2f241f6bf800
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398437(v=OCS.15)
ms:contentKeyID: 49291093
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkRegionLink

 

_**上次修改主題的時間：** 2015-03-09_

建立設定供通話許可控制 (CAC) 使用之兩個區域間的連結。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsNetworkRegionLink -NetworkRegionLinkID <String> <COMMON PARAMETERS>

    New-CsNetworkRegionLink -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -NetworkRegionID1 <String> -NetworkRegionID2 <String> [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會建立名為 NA\_EMEA 的新網路區域連結，以連結 NorthAmerica 與 EMEA 區域。此區域連結名稱會指定為 Identity 參數的值 (這會自動指派為 NetworkRegionLinkID 的值)。建立連結時需要的參數是所要連結的兩個網路區域。在此範例中，這兩個區域名稱分別是 NorthAmerica 和 EMEA。我們同時也會在此範例中指派 BWPolicyProfile 參數的值，藉此將頻寬原則設定檔 (LowBWLimits) 中所定義的頻寬限制，指派給這兩個區域間的連線。若未提供 BWPolicyProfileID，則這兩個區域之間的連線將無任何頻寬限制 (網站之間可能仍有限制。如需詳細資訊，請參閱 **New-CsNetworkSite** Cmdlet 說明主題)。

    New-CsNetworkRegionLink -Identity NA_EMEA -NetworkRegionID1 NorthAmerica -NetworkRegionID2 EMEA -BWPolicyProfileID LowBWLimits

## 詳細描述

網路中的區域是透過實體 WAN 連線相互連結。此 Cmdlet 會定義兩個區域之間的連結，並設定這些區域之間音訊和視訊連線的頻寬限制。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsNetworkRegionLink** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkRegionLink"}

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
<td><p>新建立之網路區域連結的唯一識別碼。網路區域連結只會在全域範圍建立，因此，這個識別碼不需要指定範圍。但是，它包含識別該連結之唯一名稱的字串。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>連結至由 NetworkRegionID2 參數識別之區域的 Identity (NetworkRegionID)。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>連結至由 NetworkRegionID1 參數識別之區域的 Identity (NetworkRegionID)。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinkID</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>此值與 Identity 相同。您無法同時指定 Identity 和 NetworkRegionLinkID；針對其中一個輸入的值將會自動用於兩者。</p></td>
</tr>
<tr class="odd">
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>將定義此連結頻寬限制之頻寬原則設定檔的 Identity。您可以呼叫 <strong>Get-CsNetworkBandwidthPolicyProfile</strong> Cmdlet 擷取可用的設定檔清單。</p></td>
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
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
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

此 Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkSite](new-csnetworksite.md)

