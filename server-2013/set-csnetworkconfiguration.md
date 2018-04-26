---
title: Set-CsNetworkConfiguration
TOCTitle: Set-CsNetworkConfiguration
ms:assetid: d54dc154-c092-4be9-8656-f7fec3fbd835
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398927(v=OCS.15)
ms:contentKeyID: 49292453
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改網路組態的設定。此 Cmdlet 最常用於啟用或停用通話許可控制 (CAC)。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsNetworkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfiles <PSListModifier>] [-Confirm [<SwitchParameter>]] [-EnableBandwidthPolicyCheck <$true | $false>] [-Force <SwitchParameter>] [-InterNetworkRegionRoutes <PSListModifier>] [-InterNetworkSitePolicies <PSListModifier>] [-MediaBypassSettings <MediaBypassSettingsType>] [-NetworkRegionLinks <PSListModifier>] [-NetworkRegions <PSListModifier>] [-NetworkSites <PSListModifier>] [-Subnets <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例中的命令會執行整個 CAC 組態的驗證檢查，接著再啟用 CAC (視您對傳回之警告提示的回應而定)。如果 CAC 已啟用 (亦即，如果 EnableBandwidthPolicyCheck 屬性為 True)，執行此命令僅會執行驗證檢查。

    Set-CsNetworkConfiguration -EnableBandwidthPolicyCheck $True

## 詳細描述

網路組態物件含有 Lync Server 部署中整個 CAC 組態的所有設定和媒體旁路設定。您可以使用這個 Cmdlet 來修改任何部分的 CAC 組態，而如果您需要變更媒體旁路設定，那麼就必須要使用這個 Cmdlet。不過，在修改大部分的 CAC 組態設定時，我們建議您針對特定的物件類型使用專屬的 Cmdlet。例如，在操作網路區域時，請使用以 CsNetworkRegion 一詞結尾的 Cmdlet，而避免使用此 Cmdlet 的 NetworkRegions 參數。

此 Cmdlet 的主要用途是啟用 (及停用) CAC，以及套用媒體旁路設定。在完成各種組態所需之元件 (例如區域、網站、子網路) 的設定後，您必須先啟用組態才能使其生效。若要執行此作業，只要將 EnableBandwidthPolicyCheck 參數設為 True 即可。請注意，執行此 Cmdlet 並將 EnableBandwidthPolicyCheck 設為 True，並無法立即啟用 CAC。因為在啟用 CAC 之前還必須進行一系列的驗證檢查，以確保各項設定均為適當的設定。設定中的任何錯誤或差異都會導致警告提示出現，並會詢問您，是否要在即使發生錯誤的情況下繼續啟用 CAC。如果選擇繼續 (按 Enter 鍵或 Y 鍵)，驗證作業便會繼續進行，並且會在發現其他問題時再次提示您。

如果您完成整個驗證作業並且在每次出現警告時選擇繼續，系統便會將 EnableBandwidthPolicyCheck 設為 True，而 CAC 也會隨著啟用。不過除非您解決各種問題，否則 CAC 很有可能會無法正常運作。如果您在驗證作業的任何階段中選擇停止驗證 (在警告提示中輸入 N)，驗證作業隨即會結束，而 EnableBandwidthPolicyCheck 將維持 False 的設定 (預設值)。

如果已將 EnableBandwidthPolicyCheck 設為 True，您便可呼叫 **Set-CsNetworkConfiguration** Cmdlet 並將 True 值傳遞給 EnableBandwidthPolicyCheck 參數，以執行驗證而不修改任何設定。此外，當 EnableBandwidthPolicyCheck 為 True 時，任何藉由呼叫 **Set-CsNetworkConfiguration** Cmdlet 來進行的變更嘗試都會導致驗證檢查再次執行。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsNetworkConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkConfiguration"}

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
<td><p><em>BWPolicyProfiles</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>所有可指派給網站、網站間原則及網路區域連結之頻寬原則設定檔的集合。每個頻寬原則設定檔都含有針對音訊和/或視訊連線的頻寬限制 (整體限制和工作階段限制)。完整的頻寬原則設定檔清單可藉由呼叫 <strong>Get-CsNetworkBandwidthPolicyProfile</strong> Cmdlet 來加以擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBandwidthPolicyCheck</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>將此參數設為 True 可執行整個 CAC 組態的驗證檢查。如果您通過所有驗證檢查或選擇忽略所有警告，CAC 便會啟用。如果您未通過任一項驗證檢查或選擇停止驗證，EnableBandwidthPolicyCheck 的值將不會變更。您必須定義每對網路地區之間的地區路由，再執行驗證檢查。</p>
<p>將這個值設為 False 會停用 CAC。</p>
<p>預設值：False</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>此參數不取用任何值。如有加人此參數，任何為組態所做的變更 (包括啟用組態) 都會在未顯示警告或未執行驗證檢查的情況下生效。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsIdentity</p></td>
<td><p>這個值一律是 Global。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>NetworkConfigurationSettings</p></td>
<td><p>網路組態物件的參考。這個物件必須屬於 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.SipResponseCodeTranslationRule#Decorated 類型 (可藉由呼叫 <strong>Get-CsNetworkConfiguration</strong> Cmdlet 擷取)。</p></td>
</tr>
<tr class="odd">
<td><p><em>InterNetworkRegionRoutes</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>所有在 CAC 組態中定義之網路區域路由的集合。您可以呼叫 <strong>Get-CsNetworkInterRegionRoute</strong> Cmdlet 來擷取這個集合的所有成員。</p></td>
</tr>
<tr class="even">
<td><p><em>InterNetworkSitePolicies</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>在 CAC 組態中定義之網站間原則的集合。您可以呼叫 <strong>Get-CsNetworkInterSitePolicy</strong> Cmdlet 來擷取這個集合的所有成員。</p></td>
</tr>
<tr class="odd">
<td><p><em>MediaBypassSettings</em></p></td>
<td><p>選用</p></td>
<td><p>MediaBypassSettingsType</p></td>
<td><p>一項物件參考，可定義 CAC 組態的全域媒體旁路設定。這個值的設定會覆寫所有現有的媒體旁路設定。您可以藉由呼叫 <strong>New-CsNetworkMediaBypassConfiguration</strong> Cmdlet 來取得此物件參考，並將新的組態設定指派給變數。接著再將這個變數傳遞給 MediaBypassSettings 參數以變更全域媒體旁路設定。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinks</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>在 CAC 組態中定義之網路區域連結的集合。每個網路區域連結都可定義兩個區域間的連線，以及任何應套用至這些區域間連線的頻寬限制。您可以呼叫 <strong>Get-CsNetworkRegionLink</strong> Cmdlet 來擷取這個集合的所有成員。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegions</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>在 CAC 組態中定義的網路區域集合 (每個網路區域在網路中都代表一個中樞或骨幹)。您可以呼叫 <strong>Get-CsNetworkRegion</strong> Cmdlet 來擷取這個集合的所有成員。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkSites</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>在 CAC 組態中定義的網站集合 (每個網站在區域中都代表一間辦公室或一個位置)。您可以呼叫 <strong>Get-CsNetworkSite</strong> Cmdlet 來擷取這個集合的所有成員。</p></td>
</tr>
<tr class="odd">
<td><p><em>Subnets</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>在 CAC 組態中定義的子網路集合 (每個子網路都和網站中的某個端點相關聯)。您可以呼叫 <strong>Get-CsNetworkSubnet</strong> Cmdlet 來擷取這個集合的所有成員。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.SipResponseCodeTranslationRule\#Decorated 物件。接受網路組態物件管線傳送的輸入。

## 傳回類型

**Set-CsNetworkConfiguration** Cmdlet 不會傳回值或物件，而會修改 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Remove-CsNetworkConfiguration](remove-csnetworkconfiguration.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkMediaBypassConfiguration](new-csnetworkmediabypassconfiguration.md)

