---
title: New-CsRgsHoursOfBusiness
TOCTitle: New-CsRgsHoursOfBusiness
ms:assetid: 21869ba6-526e-4c70-b84d-de73536d8a43
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398291(v=OCS.15)
ms:contentKeyID: 49290321
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsHoursOfBusiness

 

_**上次修改主題的時間：** 2015-03-09_

建立新的回應群組應用程式營業時間集。營業時間集可用以指定回應群組代理一週中可正常接聽來電的日子與時段。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsRgsHoursOfBusiness -Name <String> -Parent <RgsIdentity> [-Confirm [<SwitchParameter>]] [-Custom <$true | $false>] [-Force <SwitchParameter>] [-FridayHours1 <TimeRange>] [-FridayHours2 <TimeRange>] [-InMemory <SwitchParameter>] [-MondayHours1 <TimeRange>] [-MondayHours2 <TimeRange>] [-SaturdayHours1 <TimeRange>] [-SaturdayHours2 <TimeRange>] [-SundayHours1 <TimeRange>] [-SundayHours2 <TimeRange>] [-ThursdayHours1 <TimeRange>] [-ThursdayHours2 <TimeRange>] [-TuesdayHours1 <TimeRange>] [-TuesdayHours2 <TimeRange>] [-WednesdayHours1 <TimeRange>] [-WednesdayHours2 <TimeRange>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會在 ApplicationServer:atl-cs-001.litwareinc.com 建立名為 Help Desk Business Hours 的新營業時間集。在此範例中，不會為該營業時間集設定營業時間。

    New-CsRgsHoursOfBusiness -Parent "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "Help Desk Business Hours" 

## 範例 2

在範例 2 中，ApplicationServer:atl-cs-001.litwareinc.com 上建立了一個名為 Help Desk Business Hours 的新營業時間集。此範例會設定每個工作日 (每星期一到星期五) 的營業時間。為達此目的，範例中的第一個命令會使用 **New-CsRgsTimeRange** 命令建立下列時間範圍：OpenTime 為 8:00 AM (8:00)，CloseTime 為 6:00 PM (18:00)。此時間範圍會儲存在名為 $weekday 的變數中。

範例中的第二個命令接著會建立新的營業時間集。除了指定該營業時間集的 Parent 與 Name，會使用額外的參數 (例如 MondayHours1) 設定星期一到星期五等工作日的營業時間。每個工作日的營業時間皆會設為 8:00 A.M. 到 6:00 P.M.，且是使用時間範圍變數 $weekday 設定的。

    $weekday = New-CsRgsTimeRange -Name "Weekday Hours" -OpenTime "8:00" -CloseTime "18:00" 
    
    New-CsRgsHoursOfBusiness -Parent "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "Help Desk Business Hours" -MondayHours1 $weekday -TuesdayHours1 $weekday -WednesdayHours1 $weekday -ThursdayHours1 $weekday -FridayHours1 $weekday

## 詳細描述

為了提供給來電者最佳的服務經驗，回應群組應用程式 讓您可以清楚定義回應群組代理何時可接聽電話，何時無法接聽電話。透過 回應群組應用程式，您可以定義營業時間，這些時間指出代理在一星期的哪幾天和那些時段可接聽來電。例如，如果您組織的營業時間是星期一到星期五的 9:00 A.M. 到 5:00 P.M.，那麼您可以設定營業時間中顯示代理會在星期一到星期五的 9:00 A.M. 到 5:00 P.M. 接聽來電 (以及該分機代理無法接聽來電的時間，例如星期四 8:00 P.M. 或星期天 2:30 P.M.)。

使用 **New-CsRgsHoursOfBusiness** Cmdlet 可建立新的營業時間集。在營業時間集內設定營業時間時，請記住一星期的每一天都有 Hours1 和 Hours2 屬性。如果您服務台的服務時間是 8:00 A.M. 到 5:00 P.M.，您只需要將值指派到適當的 Hours1 屬性即可。但假設服務台的服務時間是 8:00 A.M.到 2:00 P.M.，然後再於 5:00 P.M.到 11:00 P.M.提供服務。在此狀況下，您必須將 8:00 A.M.到 2:00 P.M.的時間範圍指派給 Hours1，5:00 P.M. 到 11:00 P.M. 指派給 Hours2。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsRgsHoursOfBusiness** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsHoursOfBusiness"}

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
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指派給營業時間集的唯一名稱。Parent 屬性和 Name 屬性的組合可讓您單獨識別營業時間集，而不必參考集合的全域唯一識別碼 (GUID)。</p></td>
</tr>
<tr class="even">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>主控新營業時間集的服務。例如：-Parent &quot;service:ApplicationServer:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Custom</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True，則只有指定的工作流程會使用該營業時間。如果設為 False (預設值)，則營業時間可在多個工作流程之間共用。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>FridayHours1</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>星期五的第一個開始時間與結束時間集。假設您組織的營業時間是每星期五的 9:00 A.M. 到 5:00 P.M.，則您只須設定一個時間範圍。但如果您組織的營業時間是 8:00 A.M. 到中午，午餐休息一個小時，然後再從 1:00 P.M. 營業到 5:00 P.M.，則您必須為星期五建立兩個時間範圍。</p>
<p>如果您組織在星期五不營業，則不需設定 FridayHours1 或 FridayHours2 的值。</p></td>
</tr>
<tr class="odd">
<td><p><em>FridayHours2</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>星期五的第二個開始時間與結束時間集。假設您組織的營業時間是每星期五的 9:00 A.M. 到 5:00 P.M.，則您只須設定一個時間範圍。但如果您組織的營業時間是 8:00 A.M. 到中午，午餐休息一個小時，然後再從 1:00 P.M. 營業到 5:00 P.M.，則您必須為星期五建立兩個時間範圍。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>MondayHours1</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>星期一的第一個開始時間與結束時間集。假設您組織的營業時間是每星期一的 9:00 A.M. 到 5:00 P.M.，則您只須設定一個時間範圍。但如果您組織的營業時間是 8:00 A.M. 到中午，午餐休息一個小時，然後再從 1:00 P.M. 營業到 5:00 P.M.，則您必須為星期一建立兩個時間範圍。</p>
<p>如果您組織在星期一不營業，則不需設定 MondayHours1 或 MondayHours2 的值。</p></td>
</tr>
<tr class="even">
<td><p><em>MondayHours2</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>星期一的第二個開始時間與結束時間集。假設您組織的營業時間是每星期一的 9:00 A.M. 到 5:00 P.M.，則您只須設定一個時間範圍。但如果您組織的營業時間是 8:00 A.M. 到中午，午餐休息一個小時，然後再從 1:00 P.M. 營業到 5:00 P.M.，則您必須為星期一建立兩個時間範圍。</p></td>
</tr>
<tr class="odd">
<td><p><em>SaturdayHours1</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>星期六的第一個開始時間與結束時間集。假設您組織的營業時間是每星期六的 9:00 A.M. 到 5:00 P.M.，則您只須設定一個時間範圍。但如果您組織的營業時間是 8:00 A.M. 到中午，午餐休息一個小時，然後再從 1:00 P.M. 營業到 5:00 P.M.，則您必須為星期六建立兩個時間範圍。</p>
<p>如果您組織在星期六不營業，則不需設定 SaturdayHours1 或 SaturdayHours2 的值。</p></td>
</tr>
<tr class="even">
<td><p><em>SaturdayHours2</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>星期六的第二個開始時間與結束時間集。假設您組織的營業時間是每星期六的 9:00 A.M. 到 5:00 P.M.，則您只須設定一個時間範圍。但如果您組織的營業時間是 8:00 A.M. 到中午，午餐休息一個小時，然後再從 1:00 P.M. 營業到 5:00 P.M.，則您必須為星期六建立兩個時間範圍。</p></td>
</tr>
<tr class="odd">
<td><p><em>SundayHours1</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>星期天的第一個開始時間與結束時間集。假設您組織的營業時間是每星期日的 9:00 A.M. 到 5:00 P.M.，則您只須設定一個時間範圍。但如果您組織的營業時間是 8:00 A.M. 到中午，午餐休息一個小時，然後再從 1:00 P.M. 營業到 5:00 P.M.，則您必須為星期日建立兩個時間範圍。</p>
<p>如果您組織在星期日不營業，則不需設定 SundayHours1 或 SundayHours2 的值。</p></td>
</tr>
<tr class="even">
<td><p><em>SundayHours2</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>星期天的第二個開始時間與結束時間集。假設您組織的營業時間是每星期日的 9:00 A.M. 到 5:00 P.M.，則您只須設定一個時間範圍。但如果您組織的營業時間是 8:00 A.M. 到中午，午餐休息一個小時，然後再從 1:00 P.M. 營業到 5:00 P.M.，則您必須為星期日建立兩個時間範圍。</p></td>
</tr>
<tr class="odd">
<td><p><em>ThursdayHours1</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>星期四的第一個開始時間與結束時間集。假設您組織的營業時間是每星期四的 9:00 A.M. 到 5:00 P.M.，則您只須設定一個時間範圍。但如果您組織的營業時間是 8:00 A.M. 到中午，午餐休息一個小時，然後再從 1:00 P.M. 營業到 5:00 P.M.，則您必須為星期四建立兩個時間範圍。</p>
<p>如果您組織在星期四不營業，則不需設定 ThursdayHours1 或 ThursdayHours2 的值。</p></td>
</tr>
<tr class="even">
<td><p><em>ThursdayHours2</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>星期四的第二個開始時間與結束時間集。假設您組織的營業時間是每星期四的 9:00 A.M. 到 5:00 P.M.，則您只須設定一個時間範圍。但如果您組織的營業時間是 8:00 A.M. 到中午，午餐休息一個小時，然後再從 1:00 P.M. 營業到 5:00 P.M.，則您必須為星期四建立兩個時間範圍。</p></td>
</tr>
<tr class="odd">
<td><p><em>TuesdayHours1</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>星期二的第一個開始時間與結束時間集。假設您組織的營業時間是每星期二的 9:00 A.M. 到 5:00 P.M.，則您只須設定一個時間範圍。但如果您組織的營業時間是 8:00 A.M. 到中午，午餐休息一個小時，然後再從 1:00 P.M. 營業到 5:00 P.M.，則您必須為星期二建立兩個時間範圍。</p>
<p>如果您組織在星期二不營業，則不需設定 TuesdayHours1 或 TuesdayHours2 的值。</p></td>
</tr>
<tr class="even">
<td><p><em>TuesdayHours2</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>星期二的第二個開始時間與結束時間集。假設您組織的營業時間是每星期二的 9:00 A.M. 到 5:00 P.M.，則您只須設定一個時間範圍。但如果您組織的營業時間是 8:00 A.M. 到中午，午餐休息一個小時，然後再從 1:00 P.M. 營業到 5:00 P.M.，則您必須為星期二建立兩個時間範圍。</p></td>
</tr>
<tr class="odd">
<td><p><em>WednesdayHours1</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>星期三的第一個開始時間與結束時間集。假設您組織的營業時間是每星期三的 9:00 A.M. 到 5:00 P.M.，則您只須設定一個時間範圍。但如果您組織的營業時間是 8:00 A.M. 到中午，午餐休息一個小時，然後再從 1:00 P.M. 營業到 5:00 P.M.，則您必須為星期三建立兩個時間範圍。</p>
<p>如果您組織在星期三不營業，則不需設定 WednesdayHours1 或 WednesdayHours2 的值。</p></td>
</tr>
<tr class="even">
<td><p><em>WednesdayHours2</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>星期三的第二個開始時間與結束時間集。假設您組織的營業時間是每星期三的 9:00 A.M. 到 5:00 P.M.，則您只須設定一個時間範圍。但如果您組織的營業時間是 8:00 A.M. 到中午，午餐休息一個小時，然後再從 1:00 P.M. 營業到 5:00 P.M.，則您必須為星期三建立兩個時間範圍。</p></td>
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

無。**New-CsRgsHoursOfBusiness** 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Rgs.Management.WritableSettings.BusinessHours 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsHoursOfBusiness](get-csrgshoursofbusiness.md)  
[New-CsRgsTimeRange](new-csrgstimerange.md)  
[Remove-CsRgsHoursOfBusiness](remove-csrgshoursofbusiness.md)  
[Set-CsRgsHoursOfBusiness](set-csrgshoursofbusiness.md)

