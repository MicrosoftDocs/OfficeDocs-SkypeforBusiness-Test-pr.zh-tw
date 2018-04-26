---
title: Get-CsTrunk
TOCTitle: Get-CsTrunk
ms:assetid: c49407f2-2e03-4b8b-b51b-75b12ef87fd1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205244(v=OCS.15)
ms:contentKeyID: 49292249
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTrunk

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織所使用之 SIP 主幹的資訊。SIP 主幹會利用公用交換電話網路連線至 Lync Server 2013 的 Voice over IP 電話網路。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsTrunk [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsTrunk [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-PoolFqdn <String>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有 SIP 主幹的資訊。

    Get-CsTrunk

## 範例 2

範例 2 會傳回 Identity 為 PstnGateway:192.168.0.240 之單一 SIP 主幹的資訊。

    Get-CsTrunk -Identity "PstnGateway:192.168.0.240"

## 範例 3

範例 3 所示的命令會傳回集區 atl-cs-001.litwareinc.com 上所找到之所有 SIP 主幹的資訊。

    Get-CsTrunk -PoolFqdn "atl-cs-001.litwareinc.com"

## 範例 4

範例 4 會傳回所有可路由之 SIP 主幹的資訊。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsTrunk** Cmdlet，以傳回所有可用的 SIP 主幹集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Routable 屬性等於 (-eq) True ($True) 的主幹。

    Get-CsTrunk | Where-Object {$_.Routable -eq $True}

## 詳細描述

在 Microsoft Lync Server 2010 中，主幹會用於將外撥通話從中繼伺服器路由到 PSTN 閘道。每個閘道只有一個主幹，提高系統管理員回復外撥通話的困難度。但由於主幹與 PSTN 閘道的本質相同，所以您可以執行下列命令擷取所有主幹的資訊：

Get-CsService -PstnGateway

在 Lync Server 2013 中，現在已可將多個主幹指派給單一 PSTN 閘道；這表示閘道與主幹在本質上已有所不同。換言之，在 Lync Server 2013 中，您已無法使用 **Get-CsService** Cmdlet 來擷取各個主幹的詳細資訊，而必須改用新的 **Get-CsTrunk** Cmdlet 來傳回各個主幹的詳細資訊。

請注意，Windows PowerShell 命令列介面中的主幹資訊為唯讀。您無法使用 PowerShell 建立、刪除或修改主幹，而必須使用 Lync Server 拓撲產生器來執行這些作業。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTrunk"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Get-CsTrunk** Cmdlet 所執行的功能。

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
<td><p>可讓您使用萬用字元傳回 SIP 主幹 (或 SIP 主幹集合)。例如，若要傳回設定為 PSTN 閘道服務一部分的所有 SIP 主幹集合，請使用下列語法：</p>
<p>-Filter &quot;PstnGateway:*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要傳回之 SIP 主幹的唯一識別碼。例如：</p>
<p>–Identity &quot;PstnGateway:192.168.0.240&quot;</p>
<p>請注意，如有指定 Identity，即無法使用萬用字元。如果您必須使用萬用字元，請改為加入 Filter 參數。</p>
<p>如果未指定此參數，<strong>Get-CsTrunk</strong> Cmdlet 會傳回組織使用的所有 SIP 主幹集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>拓撲中所定義之主幹或 PSTN 閘道的完整網域名稱。例如：</p>
<p>-PoolFqdn &quot;atl-trunk-001.litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsTrunk** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsTrunk** Cmdlet 會傳回 Microsoft.Rtc.Management.Xds.DisplayPstnGateway\#Decorated 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)

