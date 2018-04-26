---
title: Set-CsTenantFederationConfiguration
TOCTitle: Set-CsTenantFederationConfiguration
ms:assetid: e13c2f55-7a68-4174-a0da-5eec8c65f64c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994080(v=OCS.15)
ms:contentKeyID: 52056242
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantFederationConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

針對您的 Microsoft Lync Online 租用戶管理同盟組態設定。這些設定可用於決定您的使用者可與哪些網域 (如有的話) 進行通訊。

**Set-CsTenantFederationConfiguration** Cmdlet 僅可用於 商務用 Skype Online。

## 語法

    Set-CsTenantFederationConfiguration [[-Identity] <XdsIdentity>] [-Tenant <Nullable`1>] [-AllowedDomains <IAllowedDomainsChoice>] [-BlockedDomains <PSListModifier>] [-AllowFederatedUsers] [-AllowPublicUsers] [-SharedSipAddressSpace] [-Force] [-Verbose] [-WhatIf] [-Confirm]Set-CsTenantFederationConfiguration [-Tenant <Nullable`1>] [-AllowedDomains <IAllowedDomainsChoice>] [-BlockedDomains <PSListModifier>] [-AllowFederatedUsers] [-AllowPublicUsers] [-SharedSipAddressSpace] [-Instance <PSObject>] [-Force] [-Verbose] [-WhatIf] [-Confirm]

## 範例

## 範例 1

範例 1 所示的命令會針對 TenantId 為 "bf19b7db-6960-41e5-a139-2aa373474354" 的租用戶停用與公用提供者進行通訊的功能。

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowPublicUsers $False

請注意，Tenant 參數為選用性質。若是省略該參數，Windows PowerShell 將根據您的連線資訊自動插入正確的租用戶識別碼。

## 範例 2

範例 2 示範如何停用組織中之所有租用戶的公用提供者通訊。為執行此操作，命令首先會呼叫 **Get-CsTenant** Cmdlet 以傳回所有可用租用戶的集合，接著將該集合傳送至 **Select-Object** Cmdlet，藉此僅挑選出集合中各個項目的 TenantId 屬性。該類租用戶識別碼的集合接著會傳送至 **ForEach-Object** Cmdlet。F**orEach-Object** Cmdlet 會接收各個租用戶識別碼並針對識別碼執行 **Set-CsTenantFederationConfiguration** Cmdlet，將各個租用戶的 AllowPublicUsers 屬性設為 False ($False)。

    Get-CsTenant | Select-Object TenantId | ForEach-Object {Set-CsTenantFederationConfiguration -Tenant $_.TenantId -AllowPublicUsers $False}

## 範例 3

在範例 3 中，會為 TenantId 是 "bf19b7db-6960-41e5-a139-2aa373474354" 之租用戶的封鎖網域清單上指派網域 fabrikam.com 為唯一網域。為執行此操作，範例中的第一個命令會使用 **New-CsEdgeDomainPattern** Cmdlet 建立 fabrikam.com 的新網域物件。此網域物件會儲存於名為 $x 的變數。

範例中的第二個命令接著會使用 **Set-CsTenantFederationConfiguration** Cmdlet 更新封鎖網域清單。使用 Replace 方法可確保既有的封鎖網域清單將會以新清單取代：也就是僅包含網域 fabrikam.com 的清單。

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Replace=$x}

## 範例 4

範例 4 所示的命令會從 TenantID 是 "bf19b7db-6960-41e5-a139-2aa373474354" 的租用戶所封鎖的網域清單中移除 fabrikam.com。為執行此操作，範例中的第一個命令會使用 **New-CsEdgeDomainPattern** Cmdlet 建立 fabrikam.com 的網域物件。產生的網域物件接著會儲存於名為 $x 的變數中。

範例中的第二個命令接著會使用 **Set-CsTenantFederationConfiguration** Cmdlet 與 Remove 方法從指定租用戶的封鎖網域清單中移除 fabrikam.com。

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Remove=$x}

## 範例 5

範例 5 所示的命令會將網域 fabrikam.com 新增至 TenantId 為 "bf19b7db-6960-41e5-a139-2aa373474354" 之租用戶所封鎖的網域清單中。為新增封鎖網域，範例中的第一個命令會使用 **New-CsEdgeDomainPattern** Cmdlet 建立 fabrikam.com 的網域物件。此物件會儲存為名為 $x 的變數中。

網域物件建立後，第二個命令接著會使用 **Set-CsTenantFederationConfiguration** Cmdlet 與 Add 方法將 fabrikam.com 新增至封鎖網域清單中所存在的任何網域。

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Add=$x}

## 範例 6

範例 6 示範如何從指定租用戶的封鎖網域清單中移除所有指派至該清單中的網域。若要執行此操作，只要加上 BlockedDomains 參數並將參數值設為 Null ($Null) 即可。此命令執行完成後，TenantID 為 "bf19b7db-6960-41e5-a139-2aa373474354" 之租用戶的封鎖網域清單將會清除。.

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $Null

## 詳細說明

同盟乃是可讓使用者與來自其他網域的使用者交換 IM 與目前狀態資訊的服務。透過 Lync Online，系統管理員可使用同盟組態設定管理：

  -   
    使用者是否可與來自其他網域的人員進行通訊；如果可以，可與之進行通訊的網域為何。

  -   
    使用者是否可與具有公用 IM 與目前狀態提供者帳戶的人員進行通訊，例如 Windows Live、AOL 以及 Yahoo。

系統管理員可使用 **Set-CsTenantFederationConfiguration** Cmdlet 啟用及停用與其他網域的同盟以及與公用提供者的同盟。此外，此 Cmdlet 可用於明確指示允許使用者與之通訊的網域及/或不允許使用者與之通訊的網域。然而，系統管理員必須使用 **Set-CsTenantPublicProvider** Cmdlet 才可指示使用者可與之通訊以及不可與之通訊的公用 IM 與目前狀態提供者。

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
<td><p><em>AllowedDomains</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.IAllowedDomainsChoice</p></td>
<td><p>代表允許使用者與之通訊的網域的網域物件 (使用 <strong>New-CsEdgeAllowList</strong> Cmdlet 或 <strong>New-CsEdgeAllowAllKnownDomains</strong> Cmdlet 建立)。若是使用 <strong>New-CsEdgeAllowAllKnownDomains</strong> Cmdlet，則使用者可與未顯示於封鎖網域清單的任何網域進行通訊。若是使用 <strong>New-CsEdgeAllowList</strong> Cmdlet，則使用者僅可與新增至允許網域清單中的網域進行通訊。</p>
<p>請注意，字串值無法直接傳遞至 AllowedDomains 參數。您必須改為使用 <strong>New-CsEdgeAllowList</strong> Cmdlet 或 <strong>New-CsEdgeAllowAllKnownDomains</strong> Cmdlet 建立物件參照，然後使用物件參照變數作為參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowFederatedUsers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，使用者將得以與來自其他網域的使用者進行通訊。若是此屬性設為 False，則無論指派至 AllowedDomains 與 BlockedDomains 的屬性值為何，使用者均無法與來自其他網域的使用者進行通訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPublicUsers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，使用者將得以與帳戶位於公用 IM 與目前狀態提供者的使用者進行通訊，例如 Windows Live、Yahoo 以及 AOL。使用者實際可與之通訊的公用提供者集合可使用 Set-CsTenantPublicProvider Cmdlet 加以管理。</p></td>
</tr>
<tr class="even">
<td><p><em>BlockedDomains</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若是 AllowedDomains 屬性設為 AllowAllKnownDomains，則使用者將可與來自封鎖網域清單所顯示以外之網域的使用者進行通訊。若是 AllowedDomains 屬性並未設為 AllowAllKnownDomains，則會略過封鎖清單，而使用者僅可與已明確新增至允許網域清單中的網域進行通訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>指定要修改的租用戶同盟組態設定集合。因為各個租用戶會限制於同盟設定的單一全域集合，所以在呼叫 <strong>Set-CsTenantFederationConfiguration</strong> Cmdlet 時無需加入此參數。若是您選擇使用 Identity 參數，您也必須加入 Tenant 參數，例如：</p>
<p>Set-CsTenantFederationConfiguration -Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Identity &quot;global&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>SharedSipAddressSpace</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，表示位於 Lync Online 的使用者會與位於內部部署版本之 Lync Server 的使用者使用相同的 SIP 網域。預設值為 False，表示兩方的使用者有不同的 SIP 網域。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要修改其同盟設定之租用戶帳戶的全域唯一識別碼 (GUID) ，例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>倘若使用的是 Windows PowerShell 遠端工作階段並僅連線至 商務用 Skype Online，則無需包含 Tenant 參數。相反地，系統將會根據您的連線資訊自動填入租用戶識別碼。Tenant 參數主要用於混合式部署。</p></td>
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

**Set-CsTenantFederationConfiguration** Cmdlet 接受以管線傳送之 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings 物件的執行個體。

## 傳回類型

無。**Set-CsTenantFederationConfiguration** Cmdlet 會修改既有的 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md)

