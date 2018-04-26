---
title: Remove-CsNetworkBandwidthPolicyProfile
TOCTitle: Remove-CsNetworkBandwidthPolicyProfile
ms:assetid: 7b1f3c8d-486c-4a7e-aa40-57893f249f66
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398609(v=OCS.15)
ms:contentKeyID: 49291409
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkBandwidthPolicyProfile

 

_**上次修改主題的時間：** 2015-03-09_

移除網路頻寬原則設定檔。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsNetworkBandwidthPolicyProfile -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會移除 Identity 為 LowBWProfile 的頻寬原則設定檔。由於 Identity 必須是唯一的，因此這最多會移除一個設定檔。

    Remove-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## 範例 2

範例 2 會從已指派 Identity 為 LowBWProfile 之頻寬原則設定檔的所有網站，移除該頻寬原則設定檔的所有參考，然後移除該設定檔。此範例的第一行是先呼叫 **Get-CsNetworkSite** Cmdlet，以擷取所有設定通話許可控制 (CAC) 的網站。接著會將此網站集合管線傳送到 **Where-Object** Cmdlet，這會只尋找 BWPolicyProfileID 等於 (-eq) LowBWProfile 的網站。然後將此縮小範圍後的集合 (只包含 BWPolicyProfileID 值為 LowBWProfile 的網站) 管線傳送到 **Set-CSNetworkSite** Cmdlet，以修改其中的每個網站，將 BWPolicyProfileID 變更為 Null ($null)。上述動作就是尋找 BWPolicyProfileID 為 LowBWProfile 的所有網站，並將該值設為 Null。至此就沒有任何網站使用 LowBWProfile 設定檔。接著對 LowBWProfile 設定檔呼叫 **Remove-CsNetworkBandwidthPolicyProfile** Cmdlet 以移除設定檔，因為我們已經知道沒有任何網站正在使用該設定檔。

若要確保網路組態中的任何位置都未使用該設定檔，請針對網站間原則及網路區域連結執行第一行中的相同步驟。

    Get-CsNetworkSite | Where-Object {$_.BWPolicyProfileID -eq "LowBWProfile"} | Set-CsNetworkSite -BWPolicyProfileID $null
    Remove-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## 詳細描述

頻寬原則是通話許可控制 (CAC) 的一部分，用來定義特定形式的頻寬限制 (在 Lync Server 中，只會指派音訊與視訊形式的頻寬限制)。此 Cmdlet 會移除這些原則的容器設定檔。

重要：如果設定檔已指派給網站 (使用 **New-CsNetworkSite** Cmdlet 或 **Set-CsNetworkSite** Cmdlet)、指派給網站間原則 (使用 **New-CsNetworkInterSitePolicy** Cmdlet 或 **Set-CsNetworkInterSitePolicy** Cmdlet)，或指派給網路區域連結 (使用 **New-CsNetworkRegionLink** Cmdlet 或 **Set-CsNetworkRegionLink** Cmdlet)，便無法移除該設定檔。如果您透過呼叫 **Remove-CsNetworkBandwidthPolicyProfile** Cmdlet 來嘗試移除該設定檔，將會收到錯誤。您必須先從所有網站、網站間原則及網路區域連結中移除該設定檔，然後才可以移除該設定檔。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsNetworkBandwidthPolicyProfile** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkBandwidthPolicyProfile"}

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
<td><p>唯一識別您要移除之頻寬原則設定檔的字串值。指定 Identity 將會至多移除一個設定檔。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType 物件。接受管線傳送的網路頻寬原則設定檔物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

