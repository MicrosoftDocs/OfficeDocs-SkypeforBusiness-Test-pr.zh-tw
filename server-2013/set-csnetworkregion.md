---
title: Set-CsNetworkRegion
TOCTitle: Set-CsNetworkRegion
ms:assetid: ffa1774b-ac60-4392-ad55-07bb887bf945
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413089(v=OCS.15)
ms:contentKeyID: 49292926
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkRegion

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的網路地區。網路區域代表企業網路中的網路集線器或骨幹。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsNetworkRegion [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkRegion [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AudioAlternatePath <$true | $false>] [-BWAlternatePaths <PSListModifier>] [-BypassID <String>] [-CentralSite <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-VideoAlternatePath <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例中會修改名為 NorthAmerica 的網路區域，並針對 Description 參數指定 "North American Region" 的值。如果 Description 已存在於 NorthAmerica 地區，此命令便會利用此值將其複寫。如果尚未設定 Description，則此命令會設定之。

    Set-CsNetworkRegion -Identity NorthAmerica -Description "North American Region"

## 範例 2

此範例會修改名為 EMEA 的網路區域，並為其指定新的視訊替代路徑設定。為達成此目的，會呼叫 **Set-CsNetworkRegion** Cmdlet 來傳送 EMEA 的 Identity。然後指定 VideoAlternatePath 參數，傳送 $False 值給它。將 VideoAlternatePath 設定為 False，表示如果沒有足夠的頻寬可供使用，視訊通話將不會路由傳送到替代路徑，就只是不會完成而已。

    Set-CsNetworkRegion -Identity EMEA -VideoAlternatePath $False

## 範例 3

範例 3 會將一組相同的替代路徑設定傳送給 Asia 網路區域，而該網路區域尚未針對 NorthAmerica 區域進行設定。此範例的第一行會擷取 NorthAmerica 網路區域的執行個體，並將它指派給變數 $a。第二行一開始會擷取 BWAlternatePaths 屬性或 NorthAmerica 區域的內容 (儲存於變數 $a 中)：$a.BWAlternatePaths。這將是 NorthAmerica 區域中所有替代路徑設定的集合。

接下來要做的是將該設定的集合傳送到 foreach 函數。Foreach 將在整個集合中循環執行，一次一個，執行下列大括號中的動作。在此例中，動作要呼叫 **Set-CsNetworkRegion** Cmdlet (其 Identity 為 Asia) 來設定 Asia 區域的屬性。下一個參數是 BWAlternatePaths。我們將 @{add=$\_} 值傳送給此參數。變數 $\_ 代表集合中目前的項目，在此案例中為目前的替代路徑。值的 @{add=} 部分會將該項目新增至適用於 Asia 區域的 BWAlternatePaths 集合。

    $a = Get-CsNetworkRegion -Identity NorthAmerica
    $a.BWAlternatePaths | foreach {Set-CsNetworkRegion -Identity Asia -BWAlternatePaths @{add=$_}}

## 詳細描述

網路區域會與跨多個地理區域的網路不同部分交互連線。每個網路區域都必須與中央網站產生關聯。中央網站是資料中心網站，通話許可控制 (CAC) 頻寬原則服務會在其上執行。使用此 Cmdlet 來修改現有的網路區域，包括判斷是否允許針對音訊和視訊連線使用替代路徑，以及將該區域內的網站關聯至略過媒體組態的設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsNetworkRegion** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkRegion\\b"}

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
<td><p><em>AudioAlternatePath</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>如果主要路徑的頻寬不足，此參數會判斷是否將透過替代路徑來路由傳送音訊通話。</p>
<p>此參數會填入 BWAlternatePaths 屬性。提供給此參數的值會儲存在 AlternatePath 屬性，以使路徑項目取代為 Audio 的 BWPolicyModality 值。</p>
<p>如果為此參數提供值，便無法指定 BWAlternatePaths 參數的值。</p>
<p>如果您的所有電話都是網際網路電話，此值必須設為 True，無論頻寬設定為何。</p></td>
</tr>
<tr class="even">
<td><p><em>BWAlternatePaths</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>物件的清單，包含當媒體要求無法利用慣用路徑完成 (例如已超過該路徑的限制) 時，是否要允許使用替代連線路徑的資訊。替代路徑物件的類型必須是 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWAlternatePathType。您可以呼叫 <strong>New-CsNetworkBWAlternatePath</strong> Cmdlet 建立此類型的物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>BypassID</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>全域唯一識別碼 (GUID)。這個 GUID 可用來將網路區域對應至 CAC 或增強型9-1-1 (E9-1-1) 網路組態內的略過媒體設定 (呼叫 <strong>New-CsNetworkMediaBypassConfiguration</strong> Cmdlet 時使用此 BypassID 值)。</p>
<p>此參數會在建立區域時 (透過呼叫 <strong>New-CsNetworkRegion</strong> Cmdlet) 自動產生。不建議變更此值。如果指定值，該值必須是 GUID 的格式 (例如，3b24a047-dce6-48b2-9f20-9fbff17ed62a)。您將收到一則確認，提示您確認要手動設定此值。</p></td>
</tr>
<tr class="even">
<td><p><em>CentralSite</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>執行頻寬原則服務的中央網站。必須啟用此服務，才能使用 CAC。此服務在前端伺服器或 Standard Edition 伺服器 上執行。</p></td>
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
<td><p>描述區域的字串。比起單獨使用 Identity 來說，此參數可用來提供更多此區域之用途的描述性說明。</p></td>
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
<td><p>您要修改之網路區域的唯一識別碼。Identity 的格式是可唯一識別該區域的字串。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>PSObject</p></td>
<td><p>網路區域物件的參照。此物件的類型必須是 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType，呼叫 <strong>Get-CsNetworkRegion</strong> Cmdlet 即可擷取此物件。</p></td>
</tr>
<tr class="even">
<td><p><em>VideoAlternatePath</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>此參數會決定適當的頻寬不存在於主要路徑時，是否要透過替代路徑路由傳送視訊通話。</p>
<p>此參數會填入 BWAlternatePaths 屬性。提供給此參數的值會儲存在 AlternatePath 屬性，以使路徑項目取代為 Video 的 BWPolicyModality 值。</p>
<p>如果為此參數提供值，便無法指定 BWAlternatePaths 參數的值。</p>
<p>如果您的所有電話都是網際網路電話，此值必須設為 True，無論頻寬設定為何。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType 物件。接受網路區域物件的管線傳送資料。

## 傳回類型

此 Cmdlet 不會傳回值，而會修改 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[New-CsNetworkBWAlternatePath](new-csnetworkbwalternatepath.md)

