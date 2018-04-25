---
title: Remove-CsNetworkConfiguration
TOCTitle: Remove-CsNetworkConfiguration
ms:assetid: d6945015-67f7-4f04-87ae-7cb977650d96
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398938(v=OCS.15)
ms:contentKeyID: 49292475
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

將 Lync Server 部署的所有網路組態設定重設為預設值。這會刪除整個通話許可控制 (CAC) 部署與相關的 E9-1-1 設定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsNetworkConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會移除所有 CAC、位置、E9-1-1 網路及媒體旁路設定。因為使用了 Confirm 參數，所以會在刪除之前提示您確認是否要刪除所有項目。

    Remove-CsNetworkConfiguration -Identity Global -Confirm

## 詳細描述

警告：執行此 Cmdlet 將會刪除整個網路組態，包括 CAC、E9-1-1 區域和網站，以及媒體旁路。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsNetworkConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>這個值必須是 Global。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。 建議您一律將此參數與此 Cmdlet 搭配使用。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.SipResponseCodeTranslationRule\#Decorated 物件。接受網路組態物件管線傳送的輸入。

## 傳回類型

這個 Cmdlet 不會傳回物件。它會移除 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.SipResponseCodeTranslationRule\#Decorated 類型的物件。

## 請參閱

#### 其他資源

[Set-CsNetworkConfiguration](set-csnetworkconfiguration.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

