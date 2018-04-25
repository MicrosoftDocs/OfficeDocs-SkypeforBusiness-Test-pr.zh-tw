---
title: Get-CsNetworkBandwidthPolicyProfile
TOCTitle: Get-CsNetworkBandwidthPolicyProfile
ms:assetid: 31784852-0cf4-4114-bf92-5eef6f346c47
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425815(v=OCS.15)
ms:contentKeyID: 49290509
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkBandwidthPolicyProfile

 

_**上次修改主題的時間：** 2015-03-09_

擷取一或多個網路頻寬原則設定檔。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsNetworkBandwidthPolicyProfile [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkBandwidthPolicyProfile [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

呼叫不含任何參數的 **Get-CsNetworkBandwidthPolicyProfile** Cmdlet，以擷取在 Lync Server 部署內定義的所有頻寬原則設定檔。

    Get-CsNetworkBandwidthPolicyProfile

## 範例 2

此範例會擷取 Identity 為 LowBWProfile 的頻寬原則設定檔。因為識別必須是唯一的，所以這最多只會傳回一個設定檔。

    Get-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## 範例 3

在此範例中，我們會使用 Filter 參數來指定一或多個要根據萬用字元字串擷取的設定檔。我們使用 \*50MB\* 字串，指示要擷取 Identity 值內任何一處包含 50MB 字串的所有頻寬原則設定檔。例如，這會擷取如 “BW profile for 50MB links”、“50MB audio limit” 和 “video limits of 50MB” 這類識別的設定檔。

    Get-CsNetworkBandwidthPolicyProfile -Filter *50MB*

## 詳細描述

頻寬原則為通話許可控制 (CAC) 的一部分，用於定義某些形式的頻寬限制 (在 Lync Server 中，只會指派音訊與視訊形式的頻寬限制)。此 Cmdlet 會為這些原則擷取一或多個容器設定檔。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsNetworkBandwidthPolicyProfile** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkBandwidthPolicyProfile"}

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
<td><p>包含萬用字元的字串，此字串用於擷取 Identity 值符合萬用字元模式的頻寬原則設定檔。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>您要擷取之頻寬原則設定檔的唯一識別字串值。指定 Identity 將最多擷取一個設定檔。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取網路頻寬原則設定檔，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

傳回 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)

