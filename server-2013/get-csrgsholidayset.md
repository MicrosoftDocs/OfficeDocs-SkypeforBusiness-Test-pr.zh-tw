---
title: Get-CsRgsHolidaySet
TOCTitle: Get-CsRgsHolidaySet
ms:assetid: eef7c046-088f-4334-808a-9036470919b1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412983(v=OCS.15)
ms:contentKeyID: 49292733
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRgsHolidaySet

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之回應群組假日集的資訊。回應群組假日集是假日的集合。例如，您有一個美國佇列的假日集 (此集合可能包含美國獨立紀念日) 和一個法國佇列的假日集。法國佇列可能只會將法國革命紀念日定義為假日，而不將美國獨立紀念日定義為假日。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsRgsHolidaySet [-Identity <RgsIdentity>] [-Name <String>] [-Owner <RgsIdentity>] [-ShowAll <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回已設定要用於組織的所有假日集的資訊。

    Get-CsRgsHolidaySet

## 範例 2

範例 2 所示的命令會傳回為 ApplicationServer:atl-cs-001.litwareinc.com 服務設定的所有假日集。

    Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com"

## 範例 3

範例 3 會傳回 ApplicationServer:atl-cs-001.litwareinc.com 服務的單一假日集：名稱為 "2013 Holidays" 的假日集。因為每個服務各有其專用名稱，所以此命令不會傳回一個以上的項目。

    Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "2013 Holidays"

## 範例 4

範例 4 會顯示在 "2013 Holidays" 假日集 (位於 ApplicationServer:atl-cs-001.litwareinc.com 服務) 中的假日詳細資訊。為達此目的，命令會先使用 **Get-CsRgsHolidaySet** 擷取指定的假日集。此集合會傳送到 **Select-Object** Cmdlet，以使用 ExpandProperty 參數來顯示此集合中每個假日的詳細資訊。

    Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "2013 Holidays"| Select-Object -ExpandProperty HolidayList

## 範例 5

範例 5 所示的命令會報告 ApplicationServer:atl-cs-001.litwareinc.com 上每個包含名為 Christmas Day 之假日的假日集識別。為達此目的，命令會先呼叫 **Get-CsRgsHolidaySet** 傳回在 ApplicationServer:atl-cs-001.litwareinc.com 上找到的所有假日集合。然後將該集合管線傳送到 **Select-Object**，以執行下列兩項作業：第一是選取 Identity 屬性，第二則是展開 HolidayList 屬性。

這兩項資訊 (Identity 和 HolidayList 內容的展開值) 接著傳送至 **Where-Object** Cmdlet；接著，**Where-Object** 會挑出假日 Name 等於 Christmas Day 的項目。最後，篩選後的集合會傳送到 **ForEach-Object** Cmdlet。此 Cmdlet 會取得集合中的每個識別，然後一個接一個的使用 **Get-CsRgsHolidaySet** 來擷取對應的假日集。整體效果是顯示所有包含名為 Christmas Day 之假日的假日集。

    Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Select-Object Identity -ExpandProperty HolidayList | Where-Object {$_.Name -eq "Christmas Day"} | ForEach-Object {Get-CsRgsHolidaySet -Identity $_.Identity}

## 詳細描述

為了提供給來電者最佳的服務經驗，回應群組應用程式讓您可以清楚定義回應群組代理何時可接聽電話，何時無法接聽電話。透過回應群組應用程式，您可以定義營業時間，這些時間指出代理在一星期的哪幾天和那些時段可接聽來電。例如，如果您組織的營業時間是星期一到星期五的 9:00 A.M. 到 5:00 P.M.，那麼您可以設定營業時間中顯示代理會在星期一到星期五的 9:00 A.M. 到 5:00 P.M. 接聽來電 (以及該分機代理無法接聽來電的時間，例如星期四 8:00 P.M. 或星期天 2:30 P.M.)。

不過，許多組織也有例外的典型工作週；例如，美商組織可能選在聖誕節或感恩節放假。為了顧及這些非典型的公休日，回應群組應用程式可讓您將某幾天指定為假日：也就是當組織通常應該營業，但因任何原因而沒有營業的日子。將使用 **New-CsRgsHoliday** Cmdlet 建立的個別假日收集在假日集中；例如，美國的假日可收集在名為 US\_Holidays 的假日集中，而日本的假日可收集在名為 Japanese\_Holidays 的假日集中。收集完成後，假日集便可以指派至回應群組工作流程。

**Get-CsRgsHolidaySet** 提供方法讓您傳回設定供組織使用之回應群組假日集的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsRgsHolidaySet** Cmdlet：RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRgsHolidaySet"}

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
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>表示在主控假日集之服務的 Identity，或是假日集的完整 Identity。如果您指定服務識別 (例如，service:ApplicationServer:atl-cs-001.litwareinc.com)，則會傳回該服務託管的所有假日集。如果您指定假日集的識別，則只會傳回指定的假日集。請注意，假日集的識別由服務識別組成，後面加上全域唯一識別碼 (GUID)；例如：service:ApplicationServer:atl-cs-001.litwareinc.com/1987d3c2-4544-489d-bbe3-59f79f530a83.</p>
<p>還有另一種方法可傳回單一假日集，就是指定服務識別，然後再包含後面加上假日集名稱的 Name 參數。這可讓您不必知道指派給該集的 GUID 為何，就能擷取特定的假日集。</p>
<p>呼叫時若未使用任何參數，<strong>Get-CsRgsHolidaySet</strong> 會傳回設定供組織使用的所有假日集。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>建立集時給予假日集的唯一名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>Owner</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>「擁有」假日集之集區的完整網域名稱。擁有者集區識別碼和假日集的集區識別碼通常一樣。然而，如果需要暫時移動假日集 (可能在災害復原程序中)，則集區識別碼將會變更。不過，擁有者識別碼會繼續指向原始集區。</p></td>
</tr>
<tr class="even">
<td><p><em>ShowAll</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會顯示所有回應群組假日集，包括擁有者集區識別碼與集區識別碼不同的那些假日集。根據預設，Get-CsRgsHolidaySet 只會傳回擁有者集區識別碼與集區識別碼相同之假日集的資訊。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsRgsHolidaySet** 不接受管線傳送的輸入。

## 傳回類型

**Get-CsRgsHolidaySet** 會傳回 Microsoft.Rtc.Rgs.Management.WritableSettings.HolidaySet 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsRgsHolidaySet](new-csrgsholidayset.md)  
[Remove-CsRgsHolidaySet](remove-csrgsholidayset.md)  
[Set-CsRgsHolidaySet](set-csrgsholidayset.md)

