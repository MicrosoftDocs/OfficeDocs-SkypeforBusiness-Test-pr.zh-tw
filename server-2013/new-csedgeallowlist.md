---
title: New-CsEdgeAllowList
TOCTitle: New-CsEdgeAllowList
ms:assetid: 21a6d546-9e03-485c-b7ec-9deb778f2b01
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994023(v=OCS.15)
ms:contentKeyID: 52056067
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeAllowList

 

_**上次修改主題的時間：** 2015-03-09_

可讓系統管理員指定允許其使用者進行通訊的網域。僅可用於 Microsoft Lync Online 的 **New-CsEdgeAllowList** Cmdlet 必須結合 **New-CsEdgeDomainPattern** Cmdlet 與 **Set-CsTenantFederationConfiguration** Cmdlet 一併使用。

## 語法

    New-CsEdgeAllowList [-AllowedDomain <PSListModifier>] [-Verbose]

## 範例

## 範例 1

範例 1 所示的命令會將 fabrikam.com 網域指派至 TenantId 為 "bf19b7db-6960-41e5-a139-2aa373474354" 之租用戶的允許網域清單。為執行此操作，範例中的第一個命令會使用 **New-CsEdgeDomainPattern** Cmdlet 建立 fabrikam.com 的網域物件；此物件會儲存於名為 $x 的變數。網域物件建立後，即會使用 **New-CsEdgeAllowList** Cmdlet 建立僅包含 fabrikam.com 網域的新允許清單。

建立允許網域清單後，接著範例中的最後一個命令會使用 **Set-CsTenantFederationConfiguration** Cmdlet 將 fabrikam.com 設為指定租用戶之允許網域清單中的唯一網域。

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

請注意，僅有混合式部署需要使用 Tenant 參數。若是僅連線至 商務用 Skype Online，則可忽略 Tenant 參數。

## 範例 2

範例 2 示範如何將多個網域新增至允許網域清單中。為執行此操作，必須多次呼叫 **New-CsEdgeDomainPattern** Cmdlet (呼叫一次可將一個網域新增至清單中)，然後將產生的網域物件儲存為個別變數。只要使用 AllowedDomain 參數並以逗號分隔變數名稱，即可將這些變數新增至由 **New-CsEdgeAllowList** Cmdlet 建立的允許清單：

$newAllowList = New-CsEdgeAllowList -AllowedDomain $x,$y

    $x = New-CsEdgeDomainPattern -Domain "contoso.com"
    $y = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x,$y
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

## 範例 3

範例 3 會將所有網域從允許網域清單中移除。為執行此操作，範例中的第一個命令會使用 **New-CsEdgeAllowList** Cmdlet 建立空白的允許網域清單，而將 AllowedDomain 屬性設為 Null 值 ($Null) 即可完成此操作。接著，將產生的物件參照 ($newAllowList) 與 **Set-CsTenantFederationConfiguration** Cmdlet 搭配使用，從 TenantId 為 "bf19b7db-6960-41e5-a139-2aa373474354" 之租用戶的允許網域清單中移除將所有網域。

    $newAllowList = New-CsEdgeAllowList -AllowedDomain $Null
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

## 詳細說明

同盟乃是可讓使用者與來自其他網域的使用者交換 IM 與目前狀態資訊的服務。透過 Lync Online，系統管理員可使用同盟組態設定管理：

  - 使用者是否可與來自其他網域的人員通訊，以及可與之進行通訊的這些網域為何。

  - 使用者是否可與具有公用 IM 與目前狀態提供者帳戶的人員進行通訊，例如 Windows Live、AOL 以及 Yahoo。

同盟有部分是以允許網域清單與封鎖網域清單來管理。允許網域清單會指定允許使用者通訊的網域；封鎖網域清單則會指定不允許使用者通訊的網域。根據預設，使用者可與任何不在封鎖清單中的網域通訊。然而，系統管理員可修改此項預設設定，將通訊限制為允許網域清單中的網域。

Lync Online 並不允許您直接修改允許清單或封鎖清單，例如，您無法使用類似下列會將代表網域名稱的字串值傳遞至允許網域清單的命令：

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains "fabrikam.com"

您必須改為使用 **New-CsEdgeAllowAllKnownDomains** Cmdlet 或 **New-CsEdgeAllowList** Cmdlet，來建立網域物件並將該網域物件傳遞至 **Set-CsTenantFederationConfiguration** Cmdlet。若要允許使用者與封鎖網域清單中所明確指定以外的所有網域進行通訊，請使用 **New-CsEdgeAllowAllKnownDomains** Cmdlet。若要將使用者通訊限制為指定的網域集合，請使用　**New-CsEdgeAllowList** Cmdlet。在此情況下，僅會允許使用者與允許網域清單中的網域通訊。

若要將單一網域 (fabrikam.com) 新增至允許網域清單，需要使用類似以下的一組命令：

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

此命令執行完畢後，將僅允許使用者與來自 fabrikam.com 網域的使用者通訊。

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
<td><p><em>AllowedDomain</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>物件參照將新增至允許網域清單的新網域 (或網域組合)。網域物件參照必須使用 <strong>New-CsEdgeDomainPattern</strong> Cmdlet 建立。如要新增多個網域物件，可以逗號分隔物件參照，例如：</p>
<p>-AllowedDomain $x,$y</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsEdgeAllowList** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsEdgeAllowList** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowList 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md)  
[New-CsEdgeDomainPattern](new-csedgedomainpattern.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

