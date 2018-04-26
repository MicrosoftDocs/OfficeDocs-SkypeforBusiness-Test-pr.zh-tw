---
title: New-CsRgsTimeRange
TOCTitle: New-CsRgsTimeRange
ms:assetid: e8abc3cc-2b13-479d-83d6-2f542fa12e45
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399040(v=OCS.15)
ms:contentKeyID: 49292670
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsTimeRange

 

_**上次修改主題的時間：** 2015-03-09_

建立新的回應群組時間範圍。回應群組應用程式會使用時間範圍指定工作日的開始時間與結束時間。例如服務台代理若只在星期日中午 12:00 到下午 5:00 提供服務，便可為星期日建立開始時間為中午 12:00 和結束時間為下午 5:00 的時間範圍。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsRgsTimeRange -CloseTime <TimeSpan> -OpenTime <TimeSpan> [-Name <String>]

## 範例

## 範例 1

範例 1 顯示如何使用 **New-CsRgsTimeRange** Cmdlet 修改現有營業時間集的屬性。此範例會先呼叫 **New-CsRgsTimeRange**，以建立名為 "Sunday hours" 的新時間範圍。此時間範圍將開始時間設為上午 8:30 (08:30)，將結束時間設為下午 1:30 (13:30)。由此命令所建立之僅存於記憶體的時間範圍會儲存在名為 $sundayHours 的變數中。

在設定時間範圍後，範例中的第二個命令會使用 **Get-CsRgsHoursOfBusiness** Cmdlet 傳回名為 Help Desk Hours 的營業時間集合 (位於 ApplicationServer:atl-cs-001.litwareinc.com 服務)。傳回的集合會儲存在名為 $y 的變數中。

在擷取集合後，命令 3 會將 SundayHours1 屬性的值設為 $sundayHours，亦即包含新建立時間範圍的物件參考。該命令完成後，接著會使用 **Set-CsRgsHoursOfBusiness** 將那些變更寫入 Help Desk Hours 營業時間集合。請注意，如果您無法呼叫 **Set-CsRgsHoursOfBusiness**，則新建的時間範圍將只存在於記憶體中，並在您關閉 Windows PowerShell 或刪除變數的 $sundayHours 時消失。如果發生這種狀況，則不會更新 Help Desk Hours 營業時間集合。

    $sundayHours = New-CsRgsTimeRange -Name "Sunday hours" -OpenTime "08:30" -CloseTime "13:30"
    $y = Get-CsRgsHoursOfBusiness -Identity Service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Hours" 
    $y.SundayHours1 = $sundayHours
    Set-CsRgsHoursOfBusiness -Instance $y

## 範例 2

範例 2 會顯示您如何建立新的回應群組時間範圍，然後在新的營業時間集中使用該時間範圍。範例的第一個命令會使用 **New-CsRgsTimeRange** Cmdlet 建立名為 Sunday Hours 的新時間範圍。範圍的 OpenTime 設為上午 8:30 ("08:30")，CloseTime 設為下午 1:30 (使用 24 小時制時 "13:30" 表示 13 個小時又 30 分鐘)。產生的時間範圍物件會儲存在名為 $sundayHours 的變數中。

在第二個命令中會使用 **New-CsRgsBusinessHours** Cmdlet 建立名為 Help Desk Hours 的新營業時間集合。在此命令中，變數 $sundayHours 會指定屬性 SundayHours1 的時間範圍。

    $sundayHours = New-CsRgsTimeRange -Name "Sunday hours" -OpenTime "08:30" -CloseTime "13:30"
    New-CsRgsHoursOfBusiness -Parent Service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Hours" -SundayHours1 $sundayHours

## 詳細描述

回應群組應用程式 會使用營業時間集合，以追蹤代理一般會在一星期的哪幾天和哪些時段接聽電話。例如，假設服務台的服務時間為每個星期一上午 7:00 到晚上 7:00 。在此情況下，您需要執行兩個動作：您必須使用 **New-CsRgsHoursOfBusiness** Cmdlet 為服務台建立營業時間集合，然後您必須修改 MondayTimeRange1 屬性指出服務台的服務時間在上午 7:00 開始、晚上 7:00 結束。

若要修改現有的營業時間集合，必須使用 **Set-CsRgsHoursOfBusiness** Cmdlet。但是您無法用該 Cmdlet 直接修改時間範圍屬性；例如，**Set-CsRgsHoursOfBusiness** 沒有與 MondayTimeRange1 屬性對應的參數。相反的若要修改營業時間集合，必須使用 **Get-CsRgsHoursOfBusiness** 擷取該集合，然後只對記憶體中的集合進行變更，最後使用 **Set-CsRgsHoursOfBusiness** 將那些變更寫入實際的營業時間集合。

通常您在變更營業時間集合時，需要變更指定日期的開始時間和/或結束時間。若要修改開始時間與結束時間，您必須使用 **New-CsRgsTimeRange** Cmdlet 指定那些時間。當您呼叫此 Cmdlet 時，結果值必須儲存在物件參考變數中。之後會使用這個變數在營業時間集合中設定開始時間與結束時間。

任何時候當您建立營業時間的新集合時，您也必須使用 **New-CsRgsTimeRange** 指定開始與結束時間。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsRgsTimeRange** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。由於此 Cmdlet 會在記憶體內建立物件，而其本身亦不會變更系統，因此任何人皆可執行。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsTimeRange"}

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
<td><p><em>CloseTime</em></p></td>
<td><p>必要</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>指出營業時間是在一天的何時結束。CloseTime 的格式應採用 24 小時制，例如若要指出營業時間是在晚上 9:00 結束，請使用此格式：-CloseTime &quot;21:00&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>OpenTime</em></p></td>
<td><p>必要</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>指出營業時間是在一天的何時開始。OpenTime 的格式應採用 24 小時制，例如若要指出營業時間是從 1:30 P.M. 開始，請使用此格式：-OpenTime &quot;13:30&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>正在建立之時間範圍的唯一識別碼。名稱的長度上限為 128 字元。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsRgsTimeRange** 不接受管線傳送的輸入。

## 傳回類型

**New-CsRgsTimeRange** 會建立 Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsRgsHoursOfBusiness](new-csrgshoursofbusiness.md)  
[Set-CsRgsHoursOfBusiness](set-csrgshoursofbusiness.md)

