---
title: Set-CsNetworkRegionLink
TOCTitle: Set-CsNetworkRegionLink
ms:assetid: b3d5d203-2aa7-4a54-93d4-30bcda391d68
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412867(v=OCS.15)
ms:contentKeyID: 49292055
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkRegionLink

 

_**上次修改主題的時間：** 2015-03-09_

修改針對通話許可控制 (CAC) 所設定之兩個網路區域間的連結。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsNetworkRegionLink [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkRegionLink [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkRegionID1 <String>] [-NetworkRegionID2 <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例將網路區域連結的頻寬原則設定檔 NA\_EMEA 變更為設定檔 HighBWLimits。我們要修改的網路區域連結的名稱是用 Identity 參數的值指定。接著，我們將 HighBWLimits 值指定給 BWPolicyProfile 參數。這麼做會將頻寬原則設定檔 (HighBWLimits) 中定義的頻寬限制指定給這些地區間的連線。

    Set-CsNetworkRegionLink -Identity NA_EMEA -BWPolicyProfileID HighBWLimits

## 詳細描述

網路之中的地區是透過實體 WAN 連線相連結。此 Cmdlet 會修改兩個地區之間的連結，讓您變更連結的地區，以及這些地區之間的音訊和視訊連線頻寬限制。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsNetworkRegionLink** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkRegionLink"}

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
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>頻寬原則設定檔的 Identity，此頻寬原則設定檔定義此連結的限制。您可以呼叫 <strong>Get-CsNetworkBandwidthPolicyProfile</strong> Cmdlet 擷取可用的設定檔清單。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>您要修改之網路區域連結的唯一識別碼。網路區域連結只會建立在全域範圍，因此不需要為此識別碼指定範圍。而是用它包含的唯一名稱字串來識別該連結。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>NetworkRegionLinkType</p></td>
<td><p>指向網路區域連結的物件參考。此物件必須是 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType 類型，呼叫 <strong>Get-CsNetworkRegionLink</strong> Cmdlet 即可擷取此物件。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>地區的 Identity (NetworkRegionID)，此地區連結至 NetworkRegionID2 屬性識別的地區。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>地區的 Identity (NetworkRegionID)，此地區連結至 NetworkRegionID1 屬性識別的地區。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType 物件。接受網路區域連結物件管線傳送的輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會修改 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

