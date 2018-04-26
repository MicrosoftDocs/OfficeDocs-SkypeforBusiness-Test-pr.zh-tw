---
title: New-CsEdgeDomainPattern
TOCTitle: New-CsEdgeDomainPattern
ms:assetid: 653bc148-c22b-4ad4-afdd-17aaeaa299d2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994040(v=OCS.15)
ms:contentKeyID: 52056120
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeDomainPattern

 

_**上次修改主題的時間：** 2015-03-09_

用來指定將從啟用同盟的網域集或停用同盟的網域集內，新增或移除的網域。修改允許或封鎖網域清單時，必須使用 **New-CsEdgeDomainPattern** Cmdlet。字串值 (例如 "fabrikam.com") 無法直接傳遞到用於管理其中任一清單的 Cmdlet。

**New-CsEdgeDomainPattern** Cmdlet 僅可與 商務用 Skype Online 搭配使用。

## 語法

    New-CsEdgeDomainPattern -Domain <String> [-Verbose]

## 範例

## 範例 1

範例 1 示範如何將單一網域指派到特定租用戶的封鎖網域清單。為達此目的，範例的第一個命令會針對網域 fabrikam.com 建立網域物件，而作法是呼叫 **New-CsEdgeDomainPattern** Cmdlet，並在名為 $x 的變數中儲存結果網域物件。第二個命令接著會使用 **Set-CsTenantFederationConfiguration** Cmdlet 和 BlockedDomains 參數，將 fabrikam.com 設定為 TenantId "bf19b7db-6960-41e5-a139-2aa373474354" 的租用戶唯一封鎖的網域。

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $x

## 詳細描述

同盟是一種服務，可讓使用者與其他網域的使用者交換 IM 和目前狀態資訊。有了 商務用 Skype Online，系統管理員就能使用同盟組態設定來管理：

  - 使用者是否可以和其他網域的人員通訊，如果可以，則允許和哪些網域通訊。

  - 使用者是否可與在公用 IM 及目前狀態提供者 (如 Windows Live、AOL 和 Yahoo) 上擁有帳戶的人員通訊。

同盟的管理中有一部分是使用到允許的網域和封鎖網域清單。允許的網域清單指定使用者可通訊的網域，而封鎖網域清單則指定使用者禁止通訊的網域。依據預設，使用者可與不在封鎖清單上的任何網域通訊。不過，系統管理員可修改此預設設定，並限制為僅能與允許的網域清單中的網域通訊。

商務用 Skype Online 禁止直接修改允許的清單或封鎖清單。例如，您無法使用此類似命令，將代表網域名稱的字串值傳遞至封鎖網域清單：

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains "fabrikam.com"

反之，您必須使用 **New-CsEdgeDomainPattern** Cmdlet 建立網域物件、將該網域物件儲存在變數 (此範例為 $x) 中，然後將變數名稱傳遞至封鎖網域清單：

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $x

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
<td><p><em>Domain</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要新增至允許清單之網域的完整網域名稱，例如：</p>
<p>-Domain &quot;fabrikam.com&quot;</p>
<p>請注意，您在指定網域名稱時無法使用萬用字元。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **New-CsEdgeDomainPattern** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsEdgeDomainPattern** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DomainPattern 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md)  
[New-CsEdgeAllowList](new-csedgeallowlist.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

