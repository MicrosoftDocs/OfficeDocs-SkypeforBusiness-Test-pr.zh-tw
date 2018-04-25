---
title: New-CsRgsHoliday
TOCTitle: New-CsRgsHoliday
ms:assetid: 021c6286-207d-4924-b477-15c9a98d6fda
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398075(v=OCS.15)
ms:contentKeyID: 49289903
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsHoliday

 

_**上次修改主題的時間：** 2015-03-09_

建立新的回應群組假日。在回應群組應用程式中，假日是指指派到佇列中的代理，原本應上班而不上班，並且不會接聽來電的日子。例如，如果感恩節是美國員工的假日，則假日會設為 2013 年 11 月 22 日。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsRgsHoliday -EndDate <DateTime> -StartDate <DateTime> [-Name <String>]

## 範例

## 範例 1

範例 1 所示的命令顯示您可以如何建立新的假日 (Christmas Day)，然後將該假日指派到現有的假日集。為達此目的，範例中的第一個命令會使用 **New-CsRgsHoliday** Cmdlet 建立新的假日，這是一個只存在於記憶體中的「虛擬」假日，之後會儲存在 $christmasDay 變數中。**New-CsRgsHoliday** 會使用三個參數：StartDate，表示假日的開始日期 (12/25/2013 12:00 AM)；EndDate，表示假日的結束日期 (12/26/2013 12:00 AM)；Name，表示指定給該假日的唯一名稱。

建立新的假日後，第二個命令會使用 **Get-CsRgsHolidaySet** 從 ApplicationServer:atl-cs-001.litwareinc.com 服務中擷取 "2013 Holidays" 假日集。此假日集儲存在 $y 變數中。

命令 3 使用新增的方法將新的假日 ($christmasDay) 新增到假日集 ($y) 的虛擬複本中。接著最後一個命令會呼叫 **Set-CsRgsHolidaySet** 將變更 (也就是新增假日) 寫入到 ApplicationServer:atl-cs-001.litwareinc.com 服務。

    $christmasDay = New-CsRgsHoliday -StartDate "12/25/2013 12:00 AM" -EndDate "12/26/2013 12:00 AM" -Name "Christmas Day"
    $y = Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com"  -Name "2013 Holidays"
    $y.HolidayList.Add($christmasDay)
    Set-CsRgsHolidaySet -Instance $y

## 詳細描述

回應群組應用程式 會使用營業時間集合表示代理例行會在星期幾接聽電話，以及接聽電話的時間。例如，假設您的服務台通常是每個星期一的 7:00 A.M. 到 7:00 P.M. 有人。在此情況下，您可以為服務台建立一個營業時間集合，然後設定開始時間為一般星期一的 7:00 A.M.，而結束時間為 7:00 P.M.。

但是服務台人員編制為每星期一的 7:00 A.M. 到 7:00 P.M. 的這項規則可能會有例外的時候。例如在美國 7 月 4 日是假日，因此服務台人員在 7 月 4 日不會工作。為了表示服務台在 2013 年 7 月 4 日星期四不工作，您必須將這天建立成假日，然後新增到服務台假日集中。

若要建立假日，您必須使用 **New-CsRgsHoliday** 指令程式。(注意，「假日」不一定要與慶典或節日有關，假日只是代理不用接聽電話的日子)。**New-CsRgsHoliday** 不會直接將假日新增到假日集中，但 Cmdlet 會建立新的假日，新假日只存在於記憶體中。因此，您必須建立一個物件參考 (例如 $x)，這個參考會指向在記憶體中的這個執行個體。當系統已在記憶體中建立假日後，您可以使用 **Get-CsRgsHolidaySet** 指令程式擷取適當的假日集，並使用 **Set-CsRgsHolidaySet** Cmdlet 將新的假日新增到該假日集中。

雖然假日集能夠 (通常也會) 包含多個假日，但將這些假日新增至假日集時，每次只能新增一個。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsRgsHoliday** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。由於此 Cmdlet 會在記憶體內建立物件，而其本身亦不會變更系統，因此任何人皆可執行。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsHoliday\\b"}

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
<td><p><em>EndDate</em></p></td>
<td><p>必要</p></td>
<td><p>System.DateTime</p></td>
<td><p>假日的結束日期。結束日期的格式取決於您的 [地區及語言選項]。例如，在美國 2013 年 7 月 4 日的結束日期，其格式會設定如下：-EndDate &quot;7/5/2013 12:00 AM&quot;，這表示假日會在 2013 年 7 月 5 日的 12:00 A.M. 結束。</p></td>
</tr>
<tr class="even">
<td><p><em>StartDate</em></p></td>
<td><p>必要</p></td>
<td><p>System.DateTime</p></td>
<td><p>假日的開始日期。開始日期的格式取決於您的 [地區及語言選項]。例如，在美國 2013 年 7 月 4 日的開始日期，其格式會設定如下：-StartDate &quot;7/4/2013 12:00 AM&quot;，這表示假日會在 2013 年 7 月 4 日的 12:00 A.M. 開始。</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>用於區分不同假日的唯一名稱。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsRgsHoliday** 不接受管線傳送的輸入。

## 傳回類型

**New-CsRgsHoliday** 會建立 Microsoft.Rtc.Rgs.Management.WritableSettings.Holiday 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsRgsHolidaySet](new-csrgsholidayset.md)  
[Set-CsRgsHolidaySet](set-csrgsholidayset.md)

