---
title: Set-CsRgsHolidaySet
TOCTitle: Set-CsRgsHolidaySet
ms:assetid: 90848409-25a0-4cc9-a0aa-f3331b5f93e9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398736(v=OCS.15)
ms:contentKeyID: 49291657
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRgsHolidaySet

 

_**上次修改主題的時間：** 2015-03-09_

修改現有回應群組假日集的屬性值。回應群組假日集是假日的集合。例如，您有一個美國佇列的假日集 (此集合可能包含美國獨立紀念日) 和一個法國佇列的假日集。法國佇列可能只會將法國革命紀念日定義為假日，而不將美國獨立紀念日定義為假日。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsRgsHolidaySet -Instance <HolidaySet> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立新假日 (Christmas Day)，並將該假日指派至現有的假日集。為達此目的，範例中的第一個命令會使用 **New-CsRgsHoliday** Cmdlet 建立新假日 (「虛擬」假日只存在記憶體內，並會儲存在變數 $x 中)。**New-CsRgsHoliday** 會使用三個參數：StartDate 代表假日的開始日期 (12/25/2010)；EndDate 代表假日的結束日期 (12/26/2010)；Name 代表給予假日的唯一名稱。

建立新的假日後，第二個命令會使用 **Get-CsRgsHolidaySet** 從 ApplicationServer:atl-cs-001.litwareinc.com 服務中擷取名為 "2010 Holidays" 的假日集。此假日集會儲存在變數 $y 中。

命令 3 使用新增方法將新假日 ($x) 新增至假日集 ($y) 的虛擬複本。接著最後一個命令會使用 **Set-CsRgsHolidaySet** 將這些變更 (以及新增假日) 寫入 ApplicationServer:atl-cs-001.litwareinc.com 服務。

    $x = New-CsRgsHoliday -StartDate "12/25/2010" -EndDate "12/26/2010" -Name "Christmas Day"
    $y = Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "2010 Holidays"
    $y.HolidayList.Add($x)
    Set-CsRgsHolidaySet -Instance $y

## 範例 2

範例 2 中的命令從現有的假日集移除假日 (此案例為 Christmas day)。為達此目的，範例中的第一個命令會使用 **Get-CsRgsHolidaySet** 從 ApplicationServer:atl-cs-001.litwareinc.com 服務擷取假日集 2010 Holidays (-Name "2010 Holidays")，並將擷取的資料儲存在名為 $x 的變數中。

在第二個命令中，來自擷取的假日集的 HolidayList 屬性會被傳送到 **Where-Object** Cmdlet，該 Cmdlet 會挑選出名稱屬性等於 "Christmas Day" 的一個假日。該單一假日會儲存在變數 $y 中。

擷取 Christmas Day 假日之後，命令 3 會使用移除方法從假日集 ($x) 移除 Christmas Day 假日 ($y)。接著，範例中的最後一個命令使用 **Set-CsRgsHolidaySet**，將這些變更 (移除聖誕節假日) 寫入 ApplicationServer:atl-cs-001.litwareinc.com 上的實際 2010 Holidays 假日集。

    $x = Get-CsRgsHolidaySet -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "2010 Holidays"
    $y = $x.HolidayList | Where-Object {$_.Name -eq "Christmas Day"}
    $x.HolidayList.Remove($y)
    Set-CsRgsHolidaySet -Instance $x

## 範例 3

範例 3 所示的命令會從在 ApplicationServer:atl-cs-001.litwareinc.com 服務找到的假日集 "2010 Holidays" 中刪除所有假日。為達此目的，範例中的第一個命令會使用 **Get-CsRgsHolidaySet** 從 ApplicationServer:atl-cs-001.litwareinc.com 擷取合適的假日集，並將該假日集儲存在名為 $x 的變數中。

擷取假日集之後，使用清除方法移除儲存在 HolidayList 屬性中的所有值。清除此屬性之後，範例的最後一個命令會使用 **Set-CsRgsHolidaySet** Cmdlet 將這些變更寫回假日集 2010 Holidays。

    $x = Get-CsRgsHolidaySet -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "2010 Holidays"
    $x.HolidayList.Clear()
    Set-CsRgsHolidaySet -Instance $x

## 詳細描述

為了提供給來電者最佳的服務經驗，回應群組應用程式讓您可以清楚定義回應群組代理何時可接聽電話，何時無法接聽電話。透過回應群組應用程式，您可以定義營業時間來指出代理會在一星期的哪幾天和哪些時段接聽來電。例如，如果您組織的營業時間是星期一到星期五的 9:00 A.M. 到 5:00 P.M.，那麼您可以設定營業時間中顯示代理會在星期一到星期五的 9:00 A.M. 到 5:00 P.M. 接聽來電 (以及該分機代理無法接聽來電的時間，例如星期四 8:00 P.M. 或星期天 2:30 P.M.)。

不過，許多組織也有例外的典型工作週；例如，美商組織可能選在聖誕節或感恩節放假。為了顧及這些非典型的公休日，回應群組應用程式可讓您將某幾天指定為假日：組織通常會營業，但因一些原因而沒有營業的日子。將使用 **New-CsRgsHoliday** Cmdlet 建立的個別假日收集在假日集中；例如，美國的假日可收集在名為 US\_Holidays 的假日集中，而日本的假日可收集在名為 Japanese\_Holidays 的假日集中。收集完成後，假日集便可以指派至回應群組工作流程。

**Set-CsRgsHolidaySet** Cmdlet 提供您修改現有假日集的方法 (通常這表示新增假日到假日集，或從假日集中移除假日)。**Set-CsRgsHolidaySet** 不直接用來對假日集進行變更，而是使用 **Get-CsRgsHolidaySet** Cmdlet 來建立現有假日集的物件參照 (物件參照為變數，此處是指現有的假日集)。對假日集的變更是在記憶體中進行，接著使用 **Set-CsRgsHolidaySet** 將這些變更寫入實際的假日集。如果您沒有呼叫 **Set-CsRgsHolidaySet**，則您的變更只會存在於記憶體中，並在您關閉 Windows PowerShell 或刪除物件參照時消失。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsRgsHolidaySet** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRgsHolidaySet"}

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
<td><p>要修改之回應群組假日集的物件參考。物件參考通常是使用 <strong>Get-CsRgsHolidaySet</strong> Cmdlet 來擷取，並將傳回的值指派至變數；例如，此命令將物件參考傳回至佇列 Help Desk 假日集，並將該物件參考儲存在名為 $x 的變數中：</p>
<p>$x = Get-CsRgsHolidaySet -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name &quot;Help Desk&quot;</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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

**Set-CsRgsHolidaySet** 不會傳回任何物件或值。而是 Cmdlet 修改現有 Microsoft.Rtc.Rgs.Management.WritableSettings.HolidaySet 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsHolidaySet](get-csrgsholidayset.md)  
[New-CsRgsHoliday](new-csrgsholiday.md)  
[New-CsRgsHolidaySet](new-csrgsholidayset.md)  
[Remove-CsRgsHolidaySet](remove-csrgsholidayset.md)

