---
title: Remove-CsNetworkRegionLink
TOCTitle: Remove-CsNetworkRegionLink
ms:assetid: f26cde90-e789-44a7-a304-695c85e64403
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413012(v=OCS.15)
ms:contentKeyID: 49292777
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkRegionLink

 

_**上次修改主題的時間：** 2015-03-09_

移除通話許可控制 (CAC) 所設定之兩個區域間的連結。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsNetworkRegionLink -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此第一個範例會移除 Identity 為 NA\_EMEA 的網路區域連結。

    Remove-CsNetworkRegionLink -Identity NA_EMEA

## 範例 2

範例 2 會移除使用名為 HighBWLimits 之頻寬原則設定檔的所有網路區域連結。此範例會先呼叫 **Get-CsNetworkRegionLink** Cmdlet (不含任何參數)，這將會擷取所有地區連結。然後將此連結集合管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會逐一查看集合中的每個成員，檢查 BWPolicyProfileID 屬性的值。如果此屬性等於 (-eq) HighBWLimits，便會將該成員管線傳送到 **Remove-CsNetworkRegionLink** Cmdlet 移除該連結。

    Get-CsNetworkRegionLink | Where-Object {$_.BWPolicyProfileID -eq "HighBWLimits"} | Remove-CsNetworkRegionLink

## 詳細描述

網路之中的地區是透過實體 WAN 連線相連結。此 Cmdlet 不會影響任何實體連線，但確實會從 CAC 組態中移除連結。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsNetworkRegionLink** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkRegionLink"}

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
<td><p>您要移除之網路區域連結的唯一識別碼。網路區域連結只會建立在全域範圍，因此不需要為此識別碼指定範圍。而是用它包含的唯一名稱字串來識別該連結。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType 物件。接受網路區域連結物件管線傳送的輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)

