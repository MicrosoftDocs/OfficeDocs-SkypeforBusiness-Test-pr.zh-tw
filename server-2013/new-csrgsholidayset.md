---
title: New-CsRgsHolidaySet
TOCTitle: New-CsRgsHolidaySet
ms:assetid: 5c110dcf-f596-44ae-8d40-bfafc6701550
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398403(v=OCS.15)
ms:contentKeyID: 49291040
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsHolidaySet

 

_**上次修改主題的時間：** 2015-03-09_

建立新的回應群組假日集。回應群組假日集是假日的集合。例如，您有一個美國佇列的假日集 (此集合可能包含美國獨立紀念日) 和一個法國佇列的假日集。法國佇列可能只會將法國革命紀念日定義為假日，而不將美國獨立紀念日定義為假日。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsRgsHolidaySet -HolidayList <Collection> -Name <String> -Parent <RgsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立名為 2013 Holidays 的新假日集，並指派一個新假日(元旦) 至此假日集。為達此目的，第一個命令會使用 **New-CsRgsHoliday**，以針對元旦建立假日。**New-CsRgsHoliday** 有三個參數：StartDate 指出假日的開始日期 (1/1/2013 12:00 A.M.)；EndDate 指出假日的結束日期 (1/2/2013 12:00 A.M.)；Name 用來儲存指派給假日的名稱。產生的假日物件會儲存在 $x 變數中。

在記憶體中建立新的假日之後，請使用 **New-CsRgsHolidaySet** 在 ApplicationServer:atl-cs-001.litwareinc.com 服務上建立新假日集。此假日集的名稱會指定為 2013 Holidays (-Name "2013 Holidays")，且指派的假日會儲存在 $x 變數中：-HolidayList ($x)。如果您要指派多個假日到假日集，只需建立新假日，然後指派每一個假日至唯一的變數即可。您可以加入所有的變數名稱，並將其用為傳遞給 HolidayList 的參數值：

\-HolidayList($x, $y, $z)

    $x = New-CsRgsHoliday -StartDate "1/1/2013 12:00 AM" -EndDate "1/2/2013 12:00 AM" -Name "New Year's Day"
    New-CsRgsHolidaySet -Parent "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "2013 Holidays" -HolidayList($x)

## 詳細描述

為了提供給來電者最佳的服務經驗，回應群組應用程式 讓您可以清楚定義回應群組代理何時可接聽電話，何時無法接聽電話。透過 回應群組應用程式，您可以定義營業時間，這些營業時間指出代理在一星期的哪幾天和哪些時段可接聽來電。例如，如果您組織的營業時間是星期一到星期五的 9:00 A.M. 到 5:00 P.M.，那麼您可以設定營業時間中顯示代理會在星期一到星期五的 9:00 A.M. 到 5:00 P.M. 接聽來電 (以及該分機代理無法接聽來電的時間，例如星期四 8:00 P.M. 或星期天 2:30 P.M.)。

不過，許多組織也有例外的典型工作週；例如，美商組織可能選在聖誕節或感恩節放假。為了顧及非典型的公休日，回應群組應用程式 可讓您將某幾天指定為假日：也就是當組織通常應該營業，但因任何原因而沒有營業的日子。將使用 **New-CsRgsHoliday** Cmdlet 建立的個別假日收集在假日集中；例如，美國的假日可收集在名為 US\_Holidays 的假日集中，而日本的假日可收集在名為 Japanese\_Holidays 的假日集中。一旦收集完成，便可以將假日和對應的假日集指派至回應群組工作流程。

**New-CsRgsHolidaySet** Cmdlet 提供讓您設定供組織使用之新假日集的方法。請注意，當您建立新的假日集時，必須至少包含一個假日；您必須使用 **New-CsRgsHoliday** Cmdlet 來建立個別的假日。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsRgsHolidaySet** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsHolidaySet"}

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
<td><p><em>HolidayList</em></p></td>
<td><p>必要</p></td>
<td><p>System.Collections.ObjectModel.Collection</p></td>
<td><p>要新增至假日集的一或多個假日。您必須使用 <strong>New-CsRgsHoliday</strong> Cmdlet 來建立假日，並儲存在物件參考中。然後，這些物件參考會傳遞至 Holidays 參數，以便將假日新增至假日集。例如，此命令會建立名為 “新年”的假日，並將產生的值儲存在名為 $x 的物件參考中：</p>
<p>$x = New-CsRgsHoliday -StartDate &quot;1/1/2013 12:00 AM&quot; -EndDate &quot;1/2/2013 12:00 AM&quot; -Name &quot;New Year's Day&quot;</p>
<p>請注意，用來指定日期和時間的格式取決於您的 [地區及語言選項]。本主題展示的範例係使用「英文 (美國)」。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指派給假日集的唯一名稱。Parent 屬性和 Name 屬性的組合可讓您單獨識別假日集，而不必參考集的全域唯一識別碼 (GUID)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>主控新假日集的服務。例如：-Parent &quot;service:ApplicationServer:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsRgsHolidaySet** 不接受管線傳送的輸入。

## 傳回類型

**New-CsRgsHolidaySet** 會建立 Microsoft.Rtc.Rgs.Management.WritableSettings.HolidaySet 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsHolidaySet](get-csrgsholidayset.md)  
[New-CsRgsHoliday](new-csrgsholiday.md)  
[Remove-CsRgsHolidaySet](remove-csrgsholidayset.md)  
[Set-CsRgsHolidaySet](set-csrgsholidayset.md)

