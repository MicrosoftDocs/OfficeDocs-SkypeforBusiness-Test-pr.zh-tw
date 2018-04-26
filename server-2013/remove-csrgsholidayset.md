---
title: Remove-CsRgsHolidaySet
TOCTitle: Remove-CsRgsHolidaySet
ms:assetid: 6e1f4ec3-2f8a-4ab1-810b-3d64eecd2031
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398521(v=OCS.15)
ms:contentKeyID: 49291262
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsRgsHolidaySet

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的回應群組假日集。回應群組假日集是假日的集合。例如，您可以擁有一個美國佇列的假日集 (此集合可能包含美國獨立紀念日)，以及另一個法國佇列的假日集。後者佇列可定義法國革命紀念日為假日，而非美國獨立紀念日。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsRgsHolidaySet -Instance <HolidaySet> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會從 ApplicationServer:atl-cs-001.litwareinc.com 服務中移除假日集 "2010 Holidays"。為達此目的，命令會先呼叫 **Get-CsRgsHolidaySet** 搭配下列兩個參數：Identity 參數 (指定假日集的位置) 和 Name 參數 (指定集合的名稱)。然後再將傳回的物件管線傳送到 **Remove-CsRgsHolidaySet**，以刪除假日集 2010 Holidays。

    Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "2010 Holidays" | Remove-CsRgsHolidaySet

## 範例 2

範例 2 會刪除在 ApplicationServer:atl-cs-001.litwareinc.com 服務上的所有假日集，包含元旦假日。為達此目的，命令會先使用 **Get-CsRgsHolidaySet** 傳回在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到的所有假日集。接著，此集合會傳送到 **Select-Object** Cmdlet，以執行兩件事情：1) 選取每一個假日集的 Identity 屬性；並 2)「展開」HolidayList 屬性的值 (當展開值時，您會傳回下層物件的屬性。如果是假日，代表 Name、StartDate 和 EndDate 之類的屬性)。然後將選取的資訊 (假日集識別和假日屬性值) 管線傳送到 **Where-Object** Cmdlet，以選取 Name 等於 (-eq) "New Year's Day" 的假日集。接著將篩選後的假日集集合會再傳送到 **Remove-CsRgsHolidaySet**，以刪除包含元旦假日在內的每一個假日集。

    Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com"  | Select-Object Identity -ExpandProperty HolidayList | Where-Object {$_.Name -eq "New Year's Day"}  | Remove-CsRgsHolidaySet 

## 範例 3

範例 3 所示的命令會從 ApplicationServer:atl-cs-001.litwareinc.com 服務刪除指派少於 5 個假日的假日集。為達此目的，命令會先呼叫 **Get-CsRgsHolidaySet**，傳回在 ApplicationServer:atl-cs-001.litwareinc.com 上找到的所有假日集集合。然後再將該集合管線傳送到 **Where-Object** Cmdlet，以選取指派的假日數目 ($\_.HolidayList.Count) 小於 5 的假日集。接著將這些假日集管線傳送至 **Remove-CsRgsHolidaySet** Cmdlet 加以刪除。

    Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com"  | Where-Object {$_.HolidayList.Count -lt 5} | Remove-CsRgsHolidaySet

## 詳細描述

為了提供給來電者最佳的服務經驗，回應群組應用程式 讓您可以清楚定義回應群組代理何時可接聽電話，何時無法接聽電話。透過 回應群組應用程式，您可以定義營業時間來指出代理會在一星期的哪幾天和哪些時段接聽來電。例如，如果您組織的營業時間是星期一到星期五的 9:00 A.M. 到 5:00 P.M.，那麼您可以設定營業時間中顯示代理會在星期一到星期五的 9:00 A.M. 到 5:00 P.M. 接聽來電 (以及該分機代理無法接聽來電的時間，例如星期四 8:00 P.M. 或星期天 2:30 P.M.)。

不過，許多組織也有例外的典型工作週；例如，美商組織可能選在聖誕節或感恩節放假。為了顧及這些非典型的公休日，回應群組應用程式 可讓您將某幾天指定為假日：也就是當組織通常應該營業，但因任何原因而沒有營業的日子。將使用 **New-CsRgsHoliday** Cmdlet 建立的個別假日收集在假日集中；例如，美國的假日可收集在名為 US\_Holidays 的假日集中，而日本的假日可收集在名為 Japanese\_Holidays 的假日集中。一旦收集完成，假日與假日集便可以指派至回應群組工作流程。

**Remove-CsRgsHolidaySet** Cmdlet 可讓系統管理員移除回應群組假日集。根據預設，如果您嘗試移除目前指派給作用中工作流程的假日集，Cmdlet 會暫停，並詢問您是否確定要刪除工作流程。在您回應提示之前，命令不會繼續，也不會移除假日集。若要覆寫此提示，並移除目前已由作用中工作流程使用的假日集，請加入 Force 參數：

Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "2010 Holidays" | Remove-CsRgsHolidaySet –Force

請注意，呼叫 **Remove-CsRgsHolidaySet** 會移除整個假日集，且移除後該集就無法再使用。如果您只想從假日集移除單一假日 (例如，因為您的公司感恩節不休假)，您應該使用 **Set-CsRgsHolidaySet** 僅移除指定的假日。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsRgsHolidaySet** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsRgsHolidaySet"}

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
<td><p><em>Instance</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.HolidaySet</p></td>
<td><p>指向要移除之假日集的物件參考。將工作流程物件傳送到 <strong>Remove-CsRgsHolidaySet</strong> 時，您可以省略 Instance 參數。</p>
<p>若要使用 Instance 參數，請使用類似下列的命令：</p>
<p>$x = Get-CsRgsHolidaySet –Identity ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83</p>
<p>Remove-CsRgsHolidaySet –Instance $x</p>
<p>請注意，使用 Instance 參數時，您一次只能移除一個假日集。這表示物件參考 ($x) 不能包含多個假日集物件。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>此參數僅供測試用。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>強制移除假日集。如果設定此參數，即使假日集由作用中的工作流程所使用，它仍然會被刪除而不會有警告。如果沒有設定此參數，則系統會要求您確認是否要刪除目前指派給作用中工作流程的任何假日集。</p></td>
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

Microsoft.Rtc.Rgs.Management.WritableSettings.HolidaySet 物件。**Remove-CsRgsHolidaySet** 會接受回應群組假日集物件的管線執行個體。

## 傳回類型

**Remove-CsRgsHolidaySet** 會刪除現有的 Microsoft.Rtc.Rgs.Management.WritableSettings.HolidaySet 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsHolidaySet](get-csrgsholidayset.md)  
[New-CsRgsHolidaySet](new-csrgsholidayset.md)  
[Set-CsRgsHolidaySet](set-csrgsholidayset.md)

