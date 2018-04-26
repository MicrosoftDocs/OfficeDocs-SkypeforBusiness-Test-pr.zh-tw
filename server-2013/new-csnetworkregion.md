---
title: New-CsNetworkRegion
TOCTitle: New-CsNetworkRegion
ms:assetid: 33a8efed-23d3-4a03-bede-80f649eaa7b9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425829(v=OCS.15)
ms:contentKeyID: 49290537
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkRegion

 

_**上次修改主題的時間：** 2015-03-09_

建立新的網路區域。網路區域代表企業網路中的網路集線器或骨幹。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsNetworkRegion -NetworkRegionID <String> <COMMON PARAMETERS>

    New-CsNetworkRegion -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -CentralSite <String> [-AudioAlternatePath <$true | $false>] [-BWAlternatePaths <PSListModifier>] [-BypassID <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-VideoAlternatePath <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會建立名為 NorthAmerica 的新網路區域。區域名稱會指定成 Identity 參數的值。另外也會為選用的 Description 參數指定值，說明此區域描述由 "All North American Locations" 組成。最後，CentralSite 參數會收到此區域的 中央網站名稱值，也就是 Redmond-NA-MLS。

    New-CsNetworkRegion -Identity NorthAmerica -Description "All North American Locations" -CentralSite Redmond-NA-MLS

## 範例 2

此範例會建立一個名稱為 EMEA 的新網路區域，這個區域包含音訊替代路徑的設定。為達成此目的，我們會呼叫 **New-CsNetworkRegion** Cmdlet，以傳遞 EMEA 的 Identity。我們會指派必要參數 CentralSite 的值 (在此範例中，此區域的 中央網站名稱為 Dublin-EU-Site)，然後我們會指定 AudioAlternatePath 參數，並將 $False 值傳遞給它。將 AudioAlternatePath 設為 False 表示在無法使用適當的頻寬時，不會將音訊通話路由傳送到替代路徑，而只是無法完成這些音訊通話。

    New-CsNetworkRegion -Identity EMEA -CentralSite Dublin-EU-Site -AudioAlternatePath $False

## 範例 3

此範例所建立的網路區域與在範例 2 中建立的網路區域相同。但此範例會使用 BWAlternatePaths 參數 (而不是 AudioAlternatePath 參數) 定義替代路徑設定。範例中的第一行會呼叫 **New-CsNetworkBWAlternatePath** Cmdlet，以建立新的替代路徑。替代路徑只有兩個屬性：BWPolicyModality (必須設為 audio 或 video，在此範例中為 audio) 和 AlternatePath (必須為 True 或 False，在此範例中為 True)。我們會將此 Cmdlet (剛建立之替代路徑物件的參考) 的輸出指派為變數 $a。

在此範例的第 2 行中，我們會在建立新網路區域時，使用這個新建立的替代路徑。為達成此目的，我們會呼叫 **New-CsNetworkRegion** Cmdlet，以傳遞 EMEA 的 Identity。我們會指派必要參數 CentralSite 的值 (在此範例中，此區域的 中央網站名稱為 Dublin-EU-Site)，然後我們會指定 BWAlternatePaths 參數，並將包含剛建立之替代路徑物件的變數 ($a) 傳遞給它。

    $a = New-CsNetworkBWAlternatePath -BWPolicyModality "audio" -AlternatePath $False
    New-CsNetworkRegion -Identity EMEA -CentralSite Dublin-EU-Site -BWAlternatePaths $a

## 詳細描述

網路區域會與跨多個地理區域的網路不同部分交互連線。每個網路區域都必須與 中央網站產生關聯。 中央網站是資料中心網站，通話許可控制 (CAC) 頻寬原則服務會在其上執行。使用此 Cmdlet 來建立新的網路區域。此 Cmdlet 的參數可讓您提供設定，這些設定會決定是否允許替代路徑透過網際網路進行音訊和視訊連線，以及是否可以自動產生略過識別碼。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsNetworkRegion** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkRegion"}

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
<td><p><em>CentralSite</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>執行頻寬原則服務的 中央網站。必須啟用此服務，才能使用 CAC。此服務在 前端伺服器或 Standard Edition 伺服器 上執行。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>新建立之網路區域的唯一識別碼。區域只會在全域範圍建立，因此，這個識別碼不需要指定範圍。但是，它包含識別該區域之唯一名稱的字串。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>此值與 Identity 相同。您無法同時指定 Identity 和 NetworkRegionID；針對其中一個輸入的值將會自動用於兩者。</p></td>
</tr>
<tr class="even">
<td><p><em>AudioAlternatePath</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果主要路徑的頻寬不足，此參數會判斷是否將透過替代路徑來路由傳送音訊通話。</p>
<p>此參數會填入 BWAlternatePaths 屬性。提供給此參數的值會儲存在 AlternatePath 屬性，以使路徑項目取代為 Audio 的 BWPolicyModality 值。</p>
<p>如果為此參數提供值，便無法指定 BWAlternatePaths 參數的值。</p>
<p>預設值：True。只有在您需要針對網際網路關閉卸載時，才將此參數設定為 False。如果您的所有電話都是網際網路電話，此值必須設為 True，無論頻寬設定為何。</p></td>
</tr>
<tr class="odd">
<td><p><em>BWAlternatePaths</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>物件清單，這些物件中包含媒體要求無法沿著慣用路徑完成 (例如，如果已經超出該路徑的限制) 時，是否允許替代網際網路連線路徑的資訊。您必須呼叫 <strong>New-CsNetworkBWAlternatePath</strong> 來建立替代路徑物件。</p>
<p>如果您提供此參數的值，您就無法提供 AudioAlternatePath 或 VideoAlternatePath 參數的值。</p>
<p>預設會啟用音訊和視訊的替代路徑 (AlternatePath = True)。</p></td>
</tr>
<tr class="even">
<td><p><em>BypassID</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>全域唯一識別碼 (GUID)。這個 GUID 可用來將網路區域對應至 CAC 或增強型9-1-1 (E9-1-1) 網路組態內的略過媒體設定 (呼叫 <strong>New-CsNetworkMediaBypassConfiguration</strong> Cmdlet 時使用此 BypassID 值)。</p>
<p>如果您不指定此參數的值，將會自動產生一個值。如果您指定一個值，則該值必須採用 GUID 的格式 (例如，3b24a047-dce6-48b2-9f20-9fbff17ed62a)。建議使用自動產生功能。如果您提供此參數的值，將會收到一個確認提示，詢問您是否確定要提供這個值，而不是讓它自動產生。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>描述區域的字串。比起單獨使用 Identity 來說，此參數可用來提供更多此區域之用途的描述性說明。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。例如，如果您提供一個值給 BypassID 參數，就不會收到確認的提示。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoAlternatePath</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數會決定適當的頻寬不存在於主要路徑時，是否要透過替代路徑路由傳送視訊通話。</p>
<p>此參數會填入 BWAlternatePaths 屬性。提供給此參數的值會儲存在 AlternatePath 屬性，以使路徑項目取代為 Video 的 BWPolicyModality 值。</p>
<p>如果為此參數提供值，便無法指定 BWAlternatePaths 參數的值。</p>
<p>預設值：True。只有在您需要針對網際網路關閉卸載時，才將此參數設定為 False。如果您的所有電話都是網際網路電話，此值必須設為 True，無論頻寬設定為何。</p></td>
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

無。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[New-CsNetworkBWAlternatePath](new-csnetworkbwalternatepath.md)

