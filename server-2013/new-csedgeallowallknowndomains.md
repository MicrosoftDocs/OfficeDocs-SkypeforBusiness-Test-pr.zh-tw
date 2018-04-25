---
title: New-CsEdgeAllowAllKnownDomains
TOCTitle: New-CsEdgeAllowAllKnownDomains
ms:assetid: f9416909-c328-41b3-9215-7ebd091b0ca0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994088(v=OCS.15)
ms:contentKeyID: 52056269
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeAllowAllKnownDomains

 

_**上次修改主題的時間：** 2015-03-09_

除了封鎖網域清單中的網域外，啟用與其他所有網域的 Microsoft Lync Online 同盟。

此 Cmdlet 僅可與 商務用 Skype Online 搭配使用。

## 語法

    New-CsEdgeAllowAllKnownDomains [-Verbose]

## 範例

## 範例 1

範例 1 所示的兩個命令會將 Identity 為 "bf19b7db-6960-41e5-a139-2aa373474354" 之租用戶的同盟設定設成允許所有已知的網域。為達此目的，範例的第一個命令會使用 **New-CsEdgeAllowAllKnownDomains** Cmdlet 來建立 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowAllKnownDomains 物件的執行個體。此執行個體會儲存在名為 $x 的變數中。第二個命令會一起呼叫 **Set-CsTenantFederationConfiguration** Cmdlet 與 AllowedDomains 參數，並使用 $x 作為參數值，將同盟設定設為允許所有已知的網域。

    $x = New-CsEdgeAllowAllKnownDomains
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $x

## 範例 2

範例 2 示範如何設定所有租用戶，以允許和未明確顯示於封鎖網域清單的所有網域通訊。為達此目的，範例的第一個命令會使用 **New-CsEdgeAllowAllKnownDomains** Cmdlet 建立 AllowAllKnownDomains 物件的執行個體 (該物件儲存於名為 $x 的變數中)。

接著，範例的第二個命令會使用 **Get-CsTenant** Cmdlet 來傳回所有可用租用戶的集合。然後，此集合會以管道方式傳送到 **ForEach-Object** Cmdlet。**ForEach-Object** Cmdlet 接下來會針對集合的每個租用戶執行 **Set-CsTenantFederationConfiguration** Cmdlet，將 AllowedDomains 屬性設定為允許所有已知的網域。

    $x = New-CsEdgeAllowAllKnownDomains
    Get-CsTenant | ForEach-Object {Set-CsTenantFederationConfiguration -Tenant $_.TenantID -AllowedDomains $x}

## 詳細描述

同盟是一種服務，可讓使用者與其他網域的使用者交換 IM 和目前狀態資訊。有了 Lync Online，系統管理員即可使用同盟組態設定來管理：

  - 使用者是否可以和其他網域的人員通訊，如果可以，則允許和哪些網域通訊。

  - 使用者是否可與在公用 IM 及目前狀態提供者 (如 Windows Live、AOL 和 Yahoo) 上擁有帳戶的人員通訊。

同盟的管理中有一部分是使用到允許的網域和封鎖網域清單。允許的網域清單指定使用者可通訊的網域，而封鎖網域清單則指定使用者禁止通訊的網域。依據預設，使用者可與不在封鎖清單上的任何網域通訊。不過，系統管理員可修改此預設設定，並限制為僅能與允許的網域清單中的網域通訊。

Lync Online 禁止直接修改允許的清單或封鎖清單，例如，您無法使用此類似命令，將代表網域名稱的字串值傳遞至允許的網域清單：

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains "fabrikam.com"

您必須改用 **New-CsEdgeAllowAllKnownDomains** Cmdlet 或 **New-CsEdgeAllowList** Cmdlet 來建立網域物件，然後將該網域物件傳遞至 **Set-CsTenantFederationConfiguration** Cmdlet。若要允許使用者與封鎖網域清單明確指定以外的所有網域通訊，請使用 **New-CsEdgeAllowAllKnownDomains** Cmdlet。若要限制使用者只能與特定一組網域通訊，請使用 N**ew-CsEdgeAllowList** Cmdlet。在該情況下，使用者僅能與允許的網域清單中顯示的網域通訊。

若要與所有已知網域設定同盟，請使用類似於以下命令的命令集：

    $x = New-CsEdgeAllowAllKnownDomains
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $x

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
<td><p>此指令程式只提供一般的 Windows PowerShell 參數。</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **New-CsEdgeAllowAllKnownDomains** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsEdgeAllowAllKnownDomains** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowAllKnownDomains 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsEdgeAllowList](new-csedgeallowlist.md)  
[New-CsEdgeDomainPattern](new-csedgedomainpattern.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

