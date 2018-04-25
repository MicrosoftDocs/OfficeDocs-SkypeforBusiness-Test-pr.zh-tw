---
title: Set-CsNetworkSite
TOCTitle: Set-CsNetworkSite
ms:assetid: 221a099c-72c4-4eb0-8812-6b2b7639a9ee
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398295(v=OCS.15)
ms:contentKeyID: 49290330
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkSite

 

_**上次修改主題的時間：** 2015-03-09_

修改針對通話許可控制 (CAC) 或增強型 9-1-1 (E9-1-1) 所定義的現有網站。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsNetworkSite [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkSite [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-BypassID <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-LocationPolicy <String>] [-NetworkRegionID <String>] [-VoiceRoutingPolicy <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

這個範例會修改名為溫哥華的網站。將要修改的網站名稱指定為 Identity 參數的值。將溫哥華網站移動到需要變更 NetworkRegionID 參數的新地區，這個範例是移動到加拿大地區。因為已提供 NetworkRegionID，但沒有為 BypassID 指定值，所以將自動產生 BypassID 值。所有先前存在的旁路識別碼都會被覆寫。

    Set-CsNetworkSite -Identity Vancouver -NetworkRegionID Canada

## 範例 2

範例 2 簡單修改與溫哥華網站相關聯的頻寬原則設定檔。將網站名稱指定為 Identity 參數的值。然後，指定 BWPolicyProfileID 參數的值：LowBWLimits。與該設定檔相關聯的原則將用於此網站。

    Set-CsNetworkSite -Identity Vancouver - BWPolicyProfileID LowBWLimits

## 詳細描述

網站是指在 CAC 或 E9-1-1 部署的每一個區域內設定的辦公室或位置。這個 Cmdlet 修改現有網站上的設定。它可以包含網站的關聯地區、網站描述，以及相關的頻寬原則設定檔。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsNetworkSite** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkSite"}

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
<td><p>頻寬原則設定檔 (可定義該網站的限制) 的 Identity。您可以呼叫 <strong>Get-CsNetworkBandwidthPolicyProfile</strong> Cmdlet 擷取可用的設定檔清單。</p>
<p>如果您指定此參數的值，您還必須指定 NetworkRegionID 參數的值。</p></td>
</tr>
<tr class="even">
<td><p><em>BypassID</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>全域唯一識別碼 (GUID)。可使用此 GUID，在 CAC 或 E9-1-1 網路組態內部將網站對應至媒體旁路設定。(呼叫 <strong>New-CsNetworkMediaBypassConfiguration</strong> Cmdlet 時使用此 BypassID 值)。</p>
<p>如果您指定此參數的值，您還必須指定 NetworkRegionID 參數的值。如果您沒有指定此參數的值，但您指定 NetworkRegionID，則會自動產生 BypassID。</p>
<p>如果您明確指定值，則必須是 GUID 格式 (例如，3b24a047-dce6-48b2-9f20-9fbff17ed62a)。建議您提供 NetworkRegionID 的值，並允許自動產生 BypassID 值。如果您手動輸入值，您會收到一個確認提示，確定您不想自動產生值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>描述網站的字串。可使用此參數提供網站適用對象的更多描述性說明，或單獨透過 Identity 表示位置。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>設為 True 時，管理語音路由會同時將使用者撥打電話及使用者接聽電話的位置納入考慮，預設值為 False。</p></td>
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
<td><p>要修改之網站的唯一識別碼。只會在全域範圍建立網站，所以您不必指定範圍。但是您必須僅指定網站 ID。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>DisplayNetworkSiteType</p></td>
<td><p>網站物件的參考 (類型 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType 的物件)。您可以呼叫 <strong>Get-CsNetworkSite</strong> Cmdlet 來擷取此物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocationPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>與這個網站相關聯的位置原則名稱。位置原則指派特定的 E9-1-1 設定至網站。呼叫 <strong>Get-CsLocationPolicy</strong> Cmdlet 可擷取位置原則清單。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>與這個網站相關聯的網路地區 Identity。如果您要提供 BypassID (透過自動產生或手動)，或網路組態的 EnableBandwidthPolicyCheck 屬性設為 True，則此參數必須包含值。您可以透過呼叫 <strong>Get-CsNetworkConfiguration</strong> Cmdlet 來擷取網路組態設定。</p>
<p>如果 BypassID 已存在於這個網站上，並且沒有指定 BypassID 參數值，則現有的 BypassID 會被自動產生的 BypassID 覆寫。</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceRoutingPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>要指派至網站的個別使用者語音路由原則。例如：</p>
<p>-VoiceRoutingPolicy &quot;RedmondVoiceRouting”</p>
<p>請注意，您必須指定每個使用者原則；無法使用 VoiceRoutingPolicy 參數將全域及/或網站原則指派至網站。</p>
<p>此參數已在 Lync Server 2013 的 2013 年 2 月版本中導入。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType 物件。接受管線傳送的網站物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會修改 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkSite](new-csnetworksite.md)  
[Remove-CsNetworkSite](remove-csnetworksite.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkMediaBypassConfiguration](new-csnetworkmediabypassconfiguration.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)

