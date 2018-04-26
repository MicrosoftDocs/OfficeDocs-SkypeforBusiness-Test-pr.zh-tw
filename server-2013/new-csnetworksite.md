---
title: New-CsNetworkSite
TOCTitle: New-CsNetworkSite
ms:assetid: 55134dd4-eb2b-483b-8b3d-e9e42ac1acc2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398365(v=OCS.15)
ms:contentKeyID: 49290952
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkSite

 

_**上次修改主題的時間：** 2015-03-09_

建立新的網站使用通話許可控制 (CAC) 或增強型 9-1-1 (E9-1-1)。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsNetworkSite -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    New-CsNetworkSite -NetworkSiteID <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -NetworkRegionID <String> [-BWPolicyProfileID <String>] [-BypassID <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-LocationPolicy <String>] [-VoiceRoutingPolicy <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

這個範例會建立名為 Vancouver 的新網站。將網站名稱指定為 Identity 參數的值。系統也會為 NetworkRegionID 參數指定值，此參數會將網站與區域 (在本例中為 NorthAmerica) 產生關聯。BypassID 值將會自動產生。我們並不建議手動設定 BypassID 值。

請注意，此範例的命令不包含 BWPolicyProfileID 參數。除非 (或直到) 日後使用 **Set-CsNetworkSite** Cmdlet 新增值，否則此網站不會有媒體連線的頻寬限制。

    New-CsNetworkSite -Identity Vancouver -NetworkRegionID NorthAmerica

## 範例 2

在範例 2 中，我們會建立一個名為 Paris 的新網站。將網站名稱指定為 Identity 參數的值。如同範例 1 所示，我們也會為 NetworkRegionID 指定值，此次是 EMEA 區域。再一次，我們正藉由允許 Cmdlet 產生 BypassID，來追隨建議的路徑。與範例 1 不同的是，這個範例也會指定 BWPolicyProfileID 參數的值：LowBWLimits。與該設定檔相關聯的原則將用於此網站。

    New-CsNetworkSite -Identity Paris -NetworkRegionID EMEA -BWPolicyProfileID LowBWLimits

## 詳細描述

網站是指在 CAC 或 E9-1-1 部署的每一個區域內設定的辦公室或位置。此 Cmdlet 會建立新的網站，並選擇性地將網站與區域產生關聯。例如，北美洲的網路區域可能會和 Chicago、Redmond 及 Vancouver等網站相關聯。您必須為組織內的每個網站建立 CAC 網站，即使該網站沒有頻寬限制。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsNetworkSite** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkSite"}

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
<td><p>新建網站的唯一識別碼。網站只會在全域範圍建立，所以此識別碼不需要指定範圍。而是包含一個在 Lync Server 部署內所有網站之間是唯一的字串。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>與這個網站相關聯的網路地區 Identity。如果您要提供 BypassID (透過自動產生或手動)，或網路組態的 EnableBandwidthPolicyCheck 屬性設為 True，則此參數必須包含值。您可以透過呼叫 <strong>Get-CsNetworkConfiguration</strong> Cmdlet 來擷取網路組態設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>這個值與 Identity 相同。您無法同時指定 Identity 與 NetworkSiteID；只要為其中之一輸入值，系統會自動將此值供這兩者使用。</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>頻寬原則設定檔 (可定義該網站的頻寬限制) 的 Identity。您可以呼叫 <strong>Get-CsNetworkBandwidthPolicyProfile</strong> Cmdlet 擷取可用的設定檔清單。</p>
<p>如果您指定此參數的值，您還必須指定 NetworkRegionID 參數的值。</p></td>
</tr>
<tr class="odd">
<td><p><em>BypassID</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>全域唯一識別碼 (GUID)。可使用此 GUID，在 CAC 或 E9-1-1 網路組態內部將網站對應至媒體旁路設定。(呼叫 <strong>New-CsNetworkMediaBypassConfiguration</strong> Cmdlet 時使用此 BypassID 值)。</p>
<p>如果您沒有為此參數指定值，則系統會自動產生值，但只有在您為 NetworkRegionID 參數提供值的情況下才會。如果您沒有提供 NetworkRegionID 參數，便不會產生 BypassID。如果您也沒有為 NetworkRegionID 參數提供值，則也無法明確為 BypassID 參數提供值。</p>
<p>如果您明確指定值，則必須是 GUID 格式 (例如，3b24a047-dce6-48b2-9f20-9fbff17ed62a)。建議自動產生。如果您手動輸入值，您會收到一個確認提示，確定您不想自動產生值。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>描述網站的字串。可使用此參數提供網站適用對象的更多描述性說明，或單獨透過 Identity 表示其位置。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，語音路由的管理將會同時考量撥打電話與接聽電話的位置。預設值為 False。</p></td>
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
<td><p><em>LocationPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>與這個網站相關聯的位置原則名稱。位置原則指派特定的 E9-1-1 設定至網站。您可以呼叫 <strong>Get-CsLocationPolicy</strong> Cmdlet 來擷取位置原則清單。</p></td>
</tr>
<tr class="even">
<td><p><em>VoiceRoutingPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要指派至網站的個別使用者語音路由原則。例如：</p>
<p>-VoiceRoutingPolicy &quot;RedmondVoiceRouting”</p>
<p>請注意，您必須指定每個使用者原則；無法使用 VoiceRoutingPolicy 參數將全域及/或網站原則指派至網站。</p>
<p>此參數已在 Lync Server 2013 的 2013 年 2 月版本中導入。</p></td>
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

建立 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsNetworkSite](remove-csnetworksite.md)  
[Set-CsNetworkSite](set-csnetworksite.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkMediaBypassConfiguration](new-csnetworkmediabypassconfiguration.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)

